## Lab Parallel Task Processing with Callable
```Java
import java.util.concurrent.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {

        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<Integer>> tasks = List.of(
            () -> { Thread.sleep(3000); return 10; },
            () -> { Thread.sleep(1000); return 20; },
            () -> { Thread.sleep(2000); return 30; }
        );

        long start = System.currentTimeMillis();

        int fastestResult = executor.invokeAny(tasks);
        System.out.println("Part B - Fastest Result: " + fastestResult);

        List<Future<Integer>> results = executor.invokeAll(tasks);
        int sum = 0;
        for (Future<Integer> f : results) {
            sum += f.get();
        }
        System.out.println("Part C - Sum of all results: " + sum);

        CompletionService<Integer> service = new ExecutorCompletionService<>(executor);
        for (Callable<Integer> task : tasks) {
            service.submit(task);
        }

        System.out.println("Part D - Results in completion order:");
        for (int i = 0; i < tasks.size(); i++) {
            Future<Integer> result = service.take();
            System.out.println(result.get());
        }

        long end = System.currentTimeMillis();
        System.out.println("Total Execution Time: " + (end - start) + "ms");

        executor.shutdown();
    }
}
```
## Reflection Questions
``` txt
Why does invokeAny return early?
It returns as soon as the first task completes successfully and cancels all other pending tasks to save resources.

When should you use invokeAll?
You should use it when you require the results from every submitted task to be finished before proceeding with the rest of your program.

How does CompletionService improve performance?
It allows you to process results immediately as they finish rather than waiting for tasks in the specific order they were submitted.

Does more threads always mean faster execution?
No, because excessive threads can lead to performance degradation due to context switching overhead and contention for limited hardware resources like CPU cores.
```

# MessageDecoder for Data Annotation Application
```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

public class MessageDecoder {
    public static void main(String[] args) {
        String url = "https://docs.google.com/document/d/e/2PACX-1vSvM5gDlNvt7npYHhp_XfsJvuntUhq184By5xO_pA4b_gCWeXb6dM6ZxwN8rE6S4ghUsCj2VKR21oEP/pub";
        decodeAndPrintGrid(url);
    }
    public static void decodeAndPrintGrid(String urlString) {
        try {
            String content = fetchUrlContent(urlString);

            List<CoordinateData> dataList = parseData(content);

            if (dataList.isEmpty()) {
                System.out.println("No data found.");
                return;
            }

            int maxX = 0;
            int maxY = 0;
            for (CoordinateData data : dataList) {
                if (data.x > maxX) maxX = data.x;
                if (data.y > maxY) maxY = data.y;
            }

            char[][] grid = new char[maxY + 1][maxX + 1];
            for (int i = 0; i <= maxY; i++) {
                for (int j = 0; j <= maxX; j++) {
                    grid[i][j] = ' ';
                }
            }

            for (CoordinateData data : dataList) {
                grid[data.y][data.x] = data.character;
            }

            for (int y = maxY; y >= 0; y--) {
                for (int x = 0; x <= maxX; x++) {
                    System.out.print(grid[y][x]);
                }
                System.out.println();
            }

        } catch (Exception e) {
            System.err.println("Error processing doc" + e.getMessage());
            e.printStackTrace();
        }
    }

    private static String fetchUrlContent(String urlString) throws Exception {
        StringBuilder result = new StringBuilder();
        URL url = new URL(urlString);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream()))) {
            for (String line; (line = reader.readLine()) != null; ) {
                result.append(line).append("\n");
            }
        }
        return result.toString();
    }

    private static List<CoordinateData> parseData(String htmlContent) {
        List<CoordinateData> list = new ArrayList<>();
                
        String[] rows = htmlContent.split("<tr[^>]*>");
        for (String row : rows) {
            String[] cells = row.split("<td[^>]*>");
            if (cells.length >= 4) {
                try {
                    String xStr = cleanHtml(cells[1]);
                    String charStr = cleanHtml(cells[2]);
                    String yStr = cleanHtml(cells[3]);

                    int x = Integer.parseInt(xStr);
                    int y = Integer.parseInt(yStr);
                    char c = charStr.isEmpty() ? ' ' : charStr.charAt(0);

                    list.add(new CoordinateData(x, y, c));
                } catch (NumberFormatException e) {
                }
            }
        }
        return list;
    }

    private static String cleanHtml(String html) {
        return html.replaceAll("<[^>]*>", "").trim();
    }

    private static class CoordinateData {
        int x, y;
        char character;

        CoordinateData(int x, int y, char character) {
            this.x = x;
            this.y = y;
            this.character = character;
        }
    }
}
```

## SalaryCalcFrame
```Java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;
import javax.swing.SwingUtilities;

public class SalaryCalcFrame extends JFrame implements ActionListener {
    private JLabel wageLabel;      // Label for hourly salary
    private JLabel hoursLabel;     // Label for hours per week
    private JLabel salLabel;       // Label for yearly salary
    private JTextField wageField;  // Input for hourly wage
    private JTextField hoursField; // Input for hours per week
    private JTextField salField;   // Displays yearly salary
    private JButton calcButton;    // Triggers calculation

    /* Constructor creates GUI components and adds them using a GridBagLayout. */
    SalaryCalcFrame() {
        GridBagConstraints layoutConst = null;

        // Set frame's title
        setTitle("Salary Calculator");

        // Initialize Labels
        wageLabel = new JLabel("Hourly wage:");
        hoursLabel = new JLabel("Hours per week:");
        salLabel = new JLabel("Yearly salary:");

        // Initialize Input Fields
        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.setText("0");

        hoursField = new JTextField(15);
        hoursField.setEditable(true);
        hoursField.setText("40");

        // Initialize Output Field
        salField = new JTextField(15);
        salField.setEditable(false);

        // Initialize Button
        calcButton = new JButton("Calculate");
        calcButton.addActionListener(this);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 10);

        // Position Wage Input
        layoutConst.gridx = 0; layoutConst.gridy = 0;
        add(wageLabel, layoutConst);
        layoutConst.gridx = 1; layoutConst.gridy = 0;
        add(wageField, layoutConst);

        // Position Hours Input
        layoutConst.gridx = 0; layoutConst.gridy = 1;
        add(hoursLabel, layoutConst);
        layoutConst.gridx = 1; layoutConst.gridy = 1;
        add(hoursField, layoutConst);

        // Position Salary Output
        layoutConst.gridx = 0; layoutConst.gridy = 2;
        add(salLabel, layoutConst);
        layoutConst.gridx = 1; layoutConst.gridy = 2;
        add(salField, layoutConst);

        // Position Calculate Button
        layoutConst.gridx = 0; layoutConst.gridy = 3;
        layoutConst.gridwidth = 2; // Span across two columns
        add(calcButton, layoutConst);
    }

    /* Method is automatically called when the "Calculate" button is pressed */
    @Override
    public void actionPerformed(ActionEvent event) {
        try {
            // Get inputs from both fields
            String wageInput = wageField.getText();
            String hoursInput = hoursField.getText();

            // Convert Strings to integers
            int hourlyWage = Integer.parseInt(wageInput);
            int hoursPerWeek = Integer.parseInt(hoursInput);

            // Calculation: Wage * Hours * 52 weeks per year
            int yearlySalary = hourlyWage * hoursPerWeek * 52;

            // Display result
            salField.setText("$" + Integer.toString(yearlySalary));
        } catch (NumberFormatException e) {
            // Simple error handling for non-numeric input
            salField.setText("Invalid Input");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            SalaryCalcFrame myFrame = new SalaryCalcFrame();
            myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            myFrame.pack();
            myFrame.setVisible(true);
        });
    }
}

```

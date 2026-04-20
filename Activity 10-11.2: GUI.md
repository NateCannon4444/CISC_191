## DistanceConverterFrame
```Java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;

public class DistanceConverterFrame extends JFrame implements ActionListener {
    private JButton calcButton;
    private JLabel distLabel;
    private JLabel kmLabel;
    private JLabel metersLabel;
    private JLabel feetLabel;
    private JTextField kmField;
    private JTextField metersField;
    private JTextField feetField;
    private JFormattedTextField distField;

    private final double MILES_TO_KM = 1.60934;
    private final double MILES_TO_METERS = 1609.34;
    private final double MILES_TO_FEET = 5280.0;

    public DistanceConverterFrame() {
        GridBagConstraints layoutConst = null;

        setTitle("Distance Unit Converter");

        distLabel = new JLabel("Distance (miles):");
        kmLabel = new JLabel("Kilometers:");
        metersLabel = new JLabel("Meters:");
        feetLabel = new JLabel("Feet:");

        calcButton = new JButton("Convert");
        calcButton.addActionListener(this);

        kmField = new JTextField(15);
        kmField.setEditable(false);

        metersField = new JTextField(15);
        metersField.setEditable(false);

        feetField = new JTextField(15);
        feetField.setEditable(false);

        distField = new JFormattedTextField(NumberFormat.getNumberInstance());
        distField.setEditable(true);
        distField.setValue(0.0);
        distField.setColumns(15);

        setLayout(new GridBagLayout());

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(distLabel, layoutConst);

        layoutConst.gridx = 1;
        add(distField, layoutConst);

        layoutConst.gridx = 2;
        add(calcButton, layoutConst);

        layoutConst.gridy = 1;
        layoutConst.gridx = 0;
        add(kmLabel, layoutConst);
        layoutConst.gridx = 1;
        add(kmField, layoutConst);

        layoutConst.gridy = 2;
        layoutConst.gridx = 0;
        add(metersLabel, layoutConst);
        layoutConst.gridx = 1;
        add(metersField, layoutConst);

        layoutConst.gridy = 3;
        layoutConst.gridx = 0;
        add(feetLabel, layoutConst);
        layoutConst.gridx = 1;
        add(feetField, layoutConst);
    }

    @Override
    public void actionPerformed(ActionEvent event) {
        double miles;

        miles = ((Number) distField.getValue()).doubleValue();

        if (miles >= 0.0) {
            double km = miles * MILES_TO_KM;
            double meters = miles * MILES_TO_METERS;
            double feet = miles * MILES_TO_FEET;

            kmField.setText(String.format("%.2f km", km));
            metersField.setText(String.format("%.2f m", meters));
            feetField.setText(String.format("%.2f ft", feet));
        } else {
            JOptionPane.showMessageDialog(this, "Please enter a positive distance.");
        }
    }

    public static void main(String[] args) {
        DistanceConverterFrame myFrame = new DistanceConverterFrame();
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```

## MilesConverter
```Java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class MilesConverter extends JFrame implements ChangeListener {
    private JSpinner milesSpinner;    
    private JTextField kmField; 
    private JLabel milesLabel;        
    private JLabel kmLabel;        

    MilesConverter() {
        int initVal = 0;
        int minVal = 0;
        int maxVal = 10000;
        int stepVal = 1;

        GridBagConstraints layoutConst = null;
        SpinnerNumberModel spinnerModel = null;

        setTitle("Distance Converter");

        milesLabel = new JLabel("Distance (miles):");
        kmLabel = new JLabel("Result (km):");

        spinnerModel = new SpinnerNumberModel(initVal, minVal, maxVal, stepVal);
        milesSpinner = new JSpinner(spinnerModel);
        milesSpinner.addChangeListener(this);

        kmField = new JTextField(15);
        kmField.setEditable(false);
        kmField.setText("0.00");

        setLayout(new GridBagLayout());

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(milesLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(milesSpinner, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(kmLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kmField, layoutConst);
    }

    @Override
    public void stateChanged(ChangeEvent event) {
        Integer miles = (Integer) milesSpinner.getValue();

        double km = miles * 1.60934;

        kmField.setText(String.format("%.2f km", km));
    }

    public static void main(String[] args) {
        MilesConverter myFrame = new MilesConverter();
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```

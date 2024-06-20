# Exercise-Locker-Application
Exercise: Locker Application
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class LockerApp extends JFrame {
    private JPasswordField passwordField;
    private JLabel statusLabel;
    private String savedPassword = null;

    public LockerApp() {
        setTitle("Lock Class");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(300, 200);
        setLayout(new BorderLayout());

        JPanel buttonPanel = new JPanel(new GridLayout(4, 3));
        JButton[] buttons = new JButton[9];
        for (int i = 0; i < 9; i++) {
            buttons[i] = new JButton(String.valueOf(i + 1));
            buttonPanel.add(buttons[i]);
            buttons[i].addActionListener(new NumberButtonListener());
        }

        JPanel controlPanel = new JPanel();
        JButton clearButton = new JButton("Clear");
        JButton enterButton = new JButton("Enter");
        clearButton.addActionListener(new ClearButtonListener());
        enterButton.addActionListener(new EnterButtonListener());
        controlPanel.add(clearButton);
        controlPanel.add(enterButton);

        passwordField = new JPasswordField(10);
        passwordField.setEditable(false);

        statusLabel = new JLabel("Enter Password");

        add(buttonPanel, BorderLayout.CENTER);
        add(controlPanel, BorderLayout.SOUTH);
        add(passwordField, BorderLayout.NORTH);
        add(statusLabel, BorderLayout.EAST);

        setVisible(true);
    }

    private class NumberButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            JButton source = (JButton) e.getSource();
            passwordField.setText(passwordField.getText() + source.getText());
        }
    }

    private class ClearButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            passwordField.setText("");
            statusLabel.setText("Enter Password");
        }
    }

    private class EnterButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            String enteredPassword = new String(passwordField.getPassword());
            if (savedPassword == null) {
                savedPassword = enteredPassword;
                statusLabel.setText("Password Set");
            } else {
                if (enteredPassword.equals(savedPassword)) {
                    statusLabel.setText("Correct Password");
                } else {
                    statusLabel.setText("Incorrect Password");
                }
            }
            passwordField.setText("");
        }
    }

    public static void main(String[] args) {
        new LockerApp();
    }
}

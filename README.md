import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class ToDoListApp extends JFrame {

    private DefaultListModel<String> taskModel;
    private JList<String> taskList;
    private JTextField taskField;
    private JButton addButton, removeButton, clearButton;

    public ToDoListApp() {

        setTitle("To-Do List Application");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        taskModel = new DefaultListModel<>();
        taskList = new JList<>(taskModel);

        JScrollPane scrollPane = new JScrollPane(taskList);

        taskField = new JTextField(20);

        addButton = new JButton("Add Task");
        removeButton = new JButton("Remove Task");
        clearButton = new JButton("Clear All");

        JPanel inputPanel = new JPanel();
        inputPanel.add(taskField);
        inputPanel.add(addButton);

        JPanel buttonPanel = new JPanel();
        buttonPanel.add(removeButton);
        buttonPanel.add(clearButton);

        add(inputPanel, BorderLayout.NORTH);
        add(scrollPane, BorderLayout.CENTER);
        add(buttonPanel, BorderLayout.SOUTH);

        // Add Task
        addButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String task = taskField.getText().trim();

                if (!task.isEmpty()) {
                    taskModel.addElement(task);
                    taskField.setText("");
                } else {
                    JOptionPane.showMessageDialog(null,
                            "Please enter a task!");
                }
            }
        });

        // Remove Selected Task
        removeButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int index = taskList.getSelectedIndex();

                if (index != -1) {
                    taskModel.remove(index);
                } else {
                    JOptionPane.showMessageDialog(null,
                            "Select a task to remove!");
                }
            }
        });

        // Clear All Tasks
        clearButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int choice = JOptionPane.showConfirmDialog(
                        null,
                        "Are you sure you want to delete all tasks?",
                        "Confirm",
                        JOptionPane.YES_NO_OPTION);

                if (choice == JOptionPane.YES_OPTION) {
                    taskModel.clear();
                }
            }
        });

        setVisible(true);
    }

    public static void main(String[] args) {
        new ToDoListApp();
    }
}

# Quiz-game
The Quiz Game GUI Application is a desktop-based interactive quiz system developed using Java Swing. The application allows users to enter their name and attempt a series of multiple-choice questions.



import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class QuizGameGUI {
    private int score = 0;
    private int questionIndex = 0;
    private String playerName;

    // Questions and answers
    private String[] questions = {
        "What does CPU stand for?",
        "Which language is used for web development?",
        "What is the brain of the computer?",
        "Who is known as the father of computer?",
        "Which protocol is used for secure websites?",
        "What does AI stand for?"
    };

    private String[][] options = {
        {"A. Central Process Unit", "B. Central Processing Unit", "C. Computer Personal Unit", "D. Control Processing Unit"},
        {"A. Python", "B. HTML", "C. C++", "D. Java"},
        {"A. RAM", "B. CPU", "C. Hard Disk", "D. GPU"},
        {"A. Alan Turing", "B. Charles Babbage", "C. Bill Gates", "D. Steve Jobs"},
        {"A. HTTP", "B. FTP", "C. HTTPS", "D. TCP"},
        {"A. Automatic Input", "B. Artificial Intelligence", "C. Advanced Internet", "D. Applied Interface"}
    };

    private String[] answers = {"B", "B", "B", "B", "C", "B"};

    private JFrame frame;
    private JLabel questionLabel;
    private JButton[] optionButtons;

    public QuizGameGUI() {
        frame = new JFrame("🎮 Quiz Game 🎮");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(500, 300);
        frame.setLayout(new BorderLayout());

        // Ask for player name
        playerName = JOptionPane.showInputDialog(frame, "Enter your name:");

        questionLabel = new JLabel("", SwingConstants.CENTER);
        questionLabel.setFont(new Font("Arial", Font.BOLD, 16));
        frame.add(questionLabel, BorderLayout.NORTH);

        JPanel buttonPanel = new JPanel(new GridLayout(2, 2));
        optionButtons = new JButton[4];

        for (int i = 0; i < 4; i++) {
            optionButtons[i] = new JButton();
            optionButtons[i].setFont(new Font("Arial", Font.PLAIN, 14));
            buttonPanel.add(optionButtons[i]);

            int index = i;
            optionButtons[i].addActionListener(e -> checkAnswer(options[questionIndex][index].substring(0,1)));
        }

        frame.add(buttonPanel, BorderLayout.CENTER);

        showQuestion();
        frame.setVisible(true);
    }

    private void showQuestion() {
        if (questionIndex < questions.length) {
            questionLabel.setText("Q" + (questionIndex+1) + ": " + questions[questionIndex]);
            for (int i = 0; i < 4; i++) {
                optionButtons[i].setText(options[questionIndex][i]);
            }
        } else {
            endGame();
        }
    }

    private void checkAnswer(String userAnswer) {
        if (userAnswer.equals(answers[questionIndex])) {
            JOptionPane.showMessageDialog(frame, "✅ Correct!");
            score++;
        } else {
            JOptionPane.showMessageDialog(frame, "❌ Wrong! Correct answer: " + answers[questionIndex]);
        }
        questionIndex++;
        showQuestion();
    }

    private void endGame() {
        String message = playerName + ", Your Total Score: " + score + "/" + questions.length + "\n";
        if (score >= 5) {
            message += "🏆 Excellent!";
        } else if (score >= 3) {
            message += "👍 Good Job!";
        } else {
            message += "📚 Keep Practicing!";
        }
        JOptionPane.showMessageDialog(frame, message);
        frame.dispose();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(QuizGameGUI::new);
    }
}

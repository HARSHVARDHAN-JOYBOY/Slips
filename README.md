import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleScrollingText extends JFrame implements ActionListener {

    private JLabel textLabel;
    private String text = "  Scrolling Text Example  "; // Text to scroll
    private int xPosition = 10; // Initial x position
    private Timer timer;
    private boolean scrollRight = true;

    public SimpleScrollingText() {
        setTitle("Simple Scrolling Text");
        setSize(400, 100);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout(FlowLayout.LEFT)); // Left flow layout

        textLabel = new JLabel(text);
        textLabel.setFont(new Font("Arial", Font.BOLD, 16));
        add(textLabel);

        timer = new Timer(50, this); // Timer every 50 milliseconds
        timer.start();

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (scrollRight) {
            xPosition += 2; // Move right by 2 pixels
            if (xPosition > getWidth()) { // If text goes off screen right
                scrollRight = false; // Change direction
                xPosition = getWidth() - 2; // Reset position to right edge (minus a bit)
            }
        } else {
            xPosition -= 2; // Move left by 2 pixels
            if (xPosition < -textLabel.getPreferredSize().width) { // If text goes off screen left
                scrollRight = true; // Change direction
                xPosition = 10; // Reset position to starting point
            }
        }
        textLabel.setLocation(xPosition, 20); // Update text position
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new SimpleScrollingText());
    }
}

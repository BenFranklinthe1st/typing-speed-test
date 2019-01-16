import javax.swing.*;
import javax.swing.text.*;
import java.awt.event.*;
import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;

/**
 * This frame will provide a graphical user interface (GUI) of the start menu, 
 * and it can open the translator class.
 * @author Frank Li
 * @date  November 18, 2018
 */
public class End extends JFrame implements ActionListener
{
        private JFrame startFrame;
        private static JTextPane textPane;
        private JPanel mainPanel;
        private JButton btnReplay;
        private StyledDocument doc;
	/**
	 * Constructor method sets up the frame for the start menu 
	 * graphical user interface
	 */

	public End(int ncpm, int nwpm, int cpm, int wpm, double a)
	{
		mainPanel = new JPanel();
		mainPanel.setBounds(0, 0, 879, 1050);
		mainPanel.setForeground(Color.WHITE);
		mainPanel.setBackground(new Color(238, 232, 170));
		mainPanel.setLayout(null);
		
		textPane = new JTextPane();
		textPane.setEditable(false);
		textPane.setBounds(63, 110, 755, 384);
		textPane.setFont(new Font("Faster One", Font.PLAIN, 60));
		mainPanel.add(textPane);
		//https://stackoverflow.com/questions/3213045/centering-text-in-a-jtextarea-or-jtextpane-horizontal-text-alignment
		doc = textPane.getStyledDocument();
		SimpleAttributeSet center = new SimpleAttributeSet();
		StyleConstants.setAlignment(center, StyleConstants.ALIGN_CENTER);
		doc.setParagraphAttributes(0, doc.getLength(), center, false);
		textPane.setText("YOUR SCORES: " + "\nNET CPM: " + ncpm + "\nNET WPM: " + nwpm + "\nCORRECT CPM: " + cpm + "\nCORRECT WPM: " + wpm +"\nACCURACY: " + a + "%");
		
		JLabel lblTitile = new JLabel("TYPING SPEED TEST");
		lblTitile.setForeground(new Color(250, 128, 114));
		lblTitile.setFont(new Font("Faster One", Font.PLAIN, 70));
		lblTitile.setHorizontalAlignment(SwingConstants.CENTER);
		lblTitile.setBounds(15, 16, 848, 60);
		mainPanel.add(lblTitile);
	
		//Set up the Jframe
		startFrame = new JFrame("Typing Speed Test");
        startFrame.setSize(900, 1075);
        startFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        startFrame.getContentPane().add(mainPanel);
        
        btnReplay = new JButton("Replay");
        btnReplay.setBounds(239, 966, 373, 37);
        btnReplay.addActionListener(this);
        mainPanel.add(btnReplay);
        
        JScrollPane scrollPane = new JScrollPane();
        scrollPane.setBounds(63, 555, 755, 395);
        mainPanel.add(scrollPane);
        
        JTextPane txtpnQA = new JTextPane();
        txtpnQA.setFont(new Font("Tahoma", Font.PLAIN, 40));
        txtpnQA.setText("Q & A\r\n\r\nWhat are CPM and WPM?\r\nThey're short for Characters Per Minute, and Words Per Minute. The \"raw CPM\" is the actual number of characters you type per minute, including all the mistakes. \"Corrected\" scores count only correctly typed words. \"WPM\" is just the corrected CPM divided by 5. That's a de facto international standard.\r\n\r\nWho are you and what's your score?\r\nHi, I'm Frank. I usually score around 260 CPM. My personal highscore is 280 CPM. This is around average.");
        scrollPane.setViewportView(txtpnQA);
        
        startFrame.setVisible(true);
		
	} 



	@Override
	public void actionPerformed(ActionEvent e) {
		
		if (e.getSource() == btnReplay) {
			startFrame.dispose();
			TypeMenu gui = new TypeMenu();
		}
		
	}
	
} // end class

import javax.swing.*;
import javax.swing.text.*;
import java.awt.event.*;
import java.awt.*;
import java.io.File;
import java.io.IOException;
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.Scanner;

/**
 * This frame will provide a graphical user interface (GUI) of the start menu, 
 * and it can open the translator class.
 * @author Frank Li
 * @date  November 18, 2018
 */
public class TypeMenu extends JFrame implements ActionListener, KeyListener
{
        private JFrame startFrame;
        private static JTextField txtType;
        private static JTextPane textPane;
        private JPanel mainPanel, keyboardPanel;
        private JButton btnRestart, btnImport;
        private static JLabel lblTime, lblWPM, lblCPM;
        private JButton[] keys;
        private JButton backspace, tab, caps, enter, lShift, rShift, spacebar;
        private char[] correctChars;
        private static String[] correctWords;
        private static ArrayList<String> typedWords = new ArrayList<String>();
        private JToggleButton keyboard;
        public boolean keyboardOn, wentBackBefore;
		public static boolean doneBefore;
        private static StyledDocument doc;
        private Style correct, incorrect;
		private static Style normal;
        private String qwerty = "`1234567890-=qwertyuiop[]\\asdfghjkl;'zxcvbnm,./ ";
        private String QWERTY = "~!@#$%^&*()_+QWERTYUIOP{}|ASDFGHJKL:\"ZXCVBNM<>? ";
        private static String text = "", prevWord;
        private int rightChar;
        private static double startTime;
        static int minute;
		static int currentChar, totalChars;
		static int numOfWords;
        static Timer time;
        static DefaultHighlighter.DefaultHighlightPainter highlightPainter = new DefaultHighlighter.DefaultHighlightPainter(Color.GREEN);
	/**
	 * Constructor method sets up the frame for the start menu 
	 * graphical user interface
	 */

	public TypeMenu()
	{
		
		mainPanel = new JPanel();
		mainPanel.setBounds(0, 0, 878, 1019);
		mainPanel.setForeground(Color.WHITE);
		mainPanel.setBackground(new Color(238, 232, 170));
		keyboardPanel = new JPanel();
		keyboardPanel.setBounds(0, 685, 876, 312);
		keyboardPanel.setVisible(false);
		mainPanel.setLayout(null);
		
		JLabel lblTitile = new JLabel("TYPING SPEED TEST");
		lblTitile.setBounds(0, 0, 876, 75);
		lblTitile.setForeground(new Color(250, 128, 114));
		lblTitile.setFont(new Font("Faster One", Font.PLAIN, 70));
		lblTitile.setHorizontalAlignment(SwingConstants.CENTER);
		mainPanel.add(lblTitile);
		
		keyboard = new JToggleButton("Keyboard");
		keyboard.setBounds(393, 640, 99, 29);
		keyboard.addItemListener(new ItemListener() {
			   public void itemStateChanged(ItemEvent ev) {
			      if(ev.getStateChange()==ItemEvent.SELECTED){
			    	  keyboardPanel.setVisible(true);
			    	  addButtons();
			    	  keyboardOn = true;
			      } else if(ev.getStateChange()==ItemEvent.DESELECTED){
			        keyboardPanel.setVisible(false);
			        keyboardOn = false;
			      }
			   }
			});
		
				txtType = new JTextField();
				txtType.setBackground(new Color(238, 238, 238));
				txtType.setBounds(0, 569, 876, 55);
				txtType.setFont(new Font("Arial", Font.PLAIN, 30));
				txtType.setHorizontalAlignment(SwingConstants.CENTER);
				txtType.setText("Type your words here");
				txtType.addKeyListener(this);
				
				JTextArea txtrIntro = new JTextArea();
				txtrIntro.setBounds(70, 80, 736, 112);
				txtrIntro.setEditable(false);
				txtrIntro.setFont(new Font("Monospaced", Font.PLAIN, 20));
				txtrIntro.setBackground(new Color(238, 232, 170));
				txtrIntro.setText("              Want to see how fast you can type? \r\n                  Finish this one-minute test.\r\n              Press the space bar after each word. \r\n  At the end, this will tell you your CPM, WPM, and accuracy.");
				mainPanel.add(txtrIntro);
				
				lblTime = new JLabel("Time: 60");
				lblTime.setBounds(657, 248, 99, 24);
				lblTime.setFont(new Font("Arial", Font.PLAIN, 20));
				mainPanel.add(lblTime);
				
				btnRestart = new JButton("Restart");
				btnRestart.setBounds(761, 241, 115, 41);
				btnRestart.addActionListener(this);
				mainPanel.add(btnRestart);
				
				textPane = new JTextPane();
				textPane.setBounds(0, 281, 876, 286);
				textPane.setEditable(false);
				textPane.setFont(new Font("Arial", Font.PLAIN, 30));
				mainPanel.add(textPane);
				//https://stackoverflow.com/questions/3213045/centering-text-in-a-jtextarea-or-jtextpane-horizontal-text-alignment
				doc = textPane.getStyledDocument();
				correct = textPane.addStyle("Green", null);
				incorrect = textPane.addStyle("Red", null);
				normal = textPane.addStyle("Black", null);
				textPane.setText(text);
				mainPanel.add(txtType);
				txtType.setColumns(10);
		mainPanel.add(keyboard);
		mainPanel.add(keyboardPanel);
		keyboardPanel.setLayout(null);
		SimpleAttributeSet center = new SimpleAttributeSet();
    	StyleConstants.setForeground(correct, Color.BLUE);
    	StyleConstants.setForeground(incorrect, Color.RED);
    	StyleConstants.setForeground(normal, Color.BLACK);
		StyleConstants.setAlignment(center, StyleConstants.ALIGN_CENTER);
		doc.setParagraphAttributes(0, doc.getLength(), center, false);
		

		try {
			IO.openInputFile("quickBrownFox.txt");
			String line = IO.readLine();
			
			while (line != null) //read out poem
			{
				text += line;
				line = IO.readLine();
			}
			IO.closeInputFile();
		} catch (IOException e) {
			e.printStackTrace();
		}
		correctChars = text.toCharArray();
		correctWords = text.split(" ");
		textPane.setText(text);
		for (int i =0;  i< correctWords.length; i++) {
			System.out.print(i + "[" + correctWords[i] + "] ");
		}
		System.out.println("");
		
		for (int i =0;  i< correctChars.length; i++) {
			System.out.print(i + "[" + correctChars[i] + "] ");
		}
		
		//Set up the Jframe
		startFrame = new JFrame("Typing Speed Test");
        startFrame.setSize(900, 1075);
        startFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        startFrame.getContentPane().add(mainPanel);
        
        btnImport = new JButton("Import your own .txt file");
        btnImport.setBounds(0, 240, 245, 42);
        btnImport.addActionListener(this);
        mainPanel.add(btnImport);
        
        lblWPM = new JLabel("WPM: 00.00");
        lblWPM.setFont(new Font("Arial", Font.PLAIN, 20));
        lblWPM.setBounds(480, 243, 122, 35);
        mainPanel.add(lblWPM);
        
        lblCPM = new JLabel("CPM: 000");
        lblCPM.setFont(new Font("Arial", Font.PLAIN, 20));
        lblCPM.setBounds(329, 243, 99, 35);
        mainPanel.add(lblCPM);
        restart();
		startFrame.setVisible(true);
		
    	try {
			textPane.getHighlighter().addHighlight(0, correctWords[numOfWords].length(), 
			        highlightPainter);
		} catch (BadLocationException b) {
			
		}
		
		time = new Timer (1000, new ActionListener() {
		     public void actionPerformed(ActionEvent evt) {
		    	 minute--;
				    if(minute == 0) //when seconds is equal to 60 then reset it to 0 and add to minutes
				    {
				    	time.stop();
				    	minute = 60;
				    	startFrame.dispose();
				    	End end = new End(getNetCPM(), getNetWPM(), getCPM(), getWPM(), getAccuracy());
				    	System.out.println(typedWords);
				    }
				    else { //until seconds is equal to 60 then prints seconds
				    	if (minute < 10) //added to make it look better, adds a 0 in front until this time is over 10
				    		lblTime.setText("Time: 0" + minute);
				    	else
				    		lblTime.setText("Time:" + minute); 	
				    }  	
		      }
		  });	
		
		 startTime = System.nanoTime();
	} 
  
	public void addButtons() {
		keys = new JButton[qwerty.length()];
		
        for (int i = 0; i < qwerty.length()-1; i++) {
            keys[i] = new JButton("" + qwerty.charAt(i));
            // new Integer('a' + i).toString()
            keys[i].setSize(60, 60);
            setPosition(i);
            keyboardPanel.add(keys[i]);
        }   
            spacebar = new JButton();
            keys[qwerty.length()-1] = spacebar;
            spacebar.setSize(300, 60);
            spacebar.setLocation(235, 240);
            keyboardPanel.add(spacebar);  
            
            backspace = new JButton("Backspace");
            backspace.setSize(98, 60);
            backspace.setLocation(780, 0);
            keyboardPanel.add(backspace); 
            
            tab = new JButton("Tab");
            tab.setSize(95, 60);
            tab.setLocation(0, 60);
            keyboardPanel.add(tab);  
            
            caps = new JButton("Caps Lock");
            caps.setSize(105, 60);
            caps.setLocation(0, 120);
            keyboardPanel.add(caps); 
           
            enter = new JButton("Enter");
            enter.setSize(113, 60);
            enter.setLocation(765, 120);
            keyboardPanel.add(enter);
            
            lShift = new JButton("lShift");
            lShift.setSize(115, 60);
            lShift.setLocation(0, 180);
            keyboardPanel.add(lShift); 
            
            rShift = new JButton("rShift");
            rShift.setSize(163, 60);
            rShift.setLocation(715, 180);
            keyboardPanel.add(rShift); 
    }
	
	public void setPosition(int i) {
        if (i <= 12) 
        	keys[i].setLocation(0 + 60*i, 0); 
        else if (i >= 13 && i < 26)
        	keys[i].setLocation(95 + 60*(i - 13), 60);
        else if (i >= 26 && i < 37) 
            keys[i].setLocation(105 + 60*(i-26), 120);
        else if (i >= 37) 
            keys[i].setLocation(115 + 60*(i-37), 180);
    }	
	
	public static void main(String[] args)
	{
		TypeMenu gui = new TypeMenu(); //open up the start menu
	}


	@Override
	public void actionPerformed(ActionEvent e) {
		
		if (e.getSource() == btnRestart) {
			time.stop();
			restart();
		}
		
		if (e.getSource() == btnImport) {
			try {
				importText();
			} catch (Exception e1) {
				// TODO Auto-generated catch block
				e1.printStackTrace();
			}
		}
		
	}
	
	public static void restart() {
		minute = 60;
		typedWords.clear();
		currentChar = 0;
		numOfWords = 0;
		totalChars = 0;
		txtType.setText("Type your words here");
		textPane.setForeground(Color.BLACK);
		lblTime.setText("Time:" + minute);
		doneBefore = false;
		doc.setCharacterAttributes(0, text.length(), normal, true); 
    	try {
    		textPane.getHighlighter().removeAllHighlights();
			textPane.getHighlighter().addHighlight(0, correctWords[numOfWords].length(), 
			        highlightPainter);
		} catch (BadLocationException b) {
			
		}
		
	}

    public void keyPressed (KeyEvent e) {
    	//time.start();

    	try {
        int i = qwerty.indexOf(e.getKeyChar());
        int c = QWERTY.indexOf(e.getKeyChar());
        if (i > 0)
        	keys[i].setBackground(Color.GREEN);
        else
        	keys[c].setBackground(Color.GREEN);
    	} catch (Exception d) {
    		
    	if (keyboardOn == true)	{
    	switch(e.getKeyCode()) {
    		case KeyEvent.VK_ENTER: enter.setBackground(Color.GREEN);
    		break;
    		case KeyEvent.VK_BACK_SPACE: backspace.setBackground(Color.GREEN);
    		break;
    		case KeyEvent.VK_TAB: tab.setBackground(Color.GREEN);
    		break;
    		case KeyEvent.VK_SHIFT: lShift.setBackground(Color.GREEN);
    		rShift.setBackground(Color.GREEN);
    		break;
    		case KeyEvent.VK_CAPS_LOCK: caps.setBackground(Color.GREEN);
    		break;
    		default: break;
    	}
    	}
    	}
    }

    public void keyReleased (KeyEvent e) {
        	
    	//doesn't run
        if (e.getKeyChar() == ' ' || e.getKeyChar() == (KeyEvent.VK_SPACE))  //in key released and not keyTyped because keyTyped adds a space after setting txtType null, but you want to et txtType null after space is pressed 
        		txtType.setText(null);

    	try {
        int i = qwerty.indexOf(e.getKeyChar());
        int c = QWERTY.indexOf(e.getKeyChar());
        if (i > 0)
        	keys[i].setBackground(null);
        else
        	keys[c].setBackground(null);
    	} catch (Exception d) {
    		
    	if (keyboardOn == true) {	
    	switch(e.getKeyCode()) {
    		case KeyEvent.VK_ENTER: enter.setBackground(null);
    		txtType.setText("");
    		break;
    		case KeyEvent.VK_BACK_SPACE: backspace.setBackground(null);
    		break;
    		case KeyEvent.VK_TAB: tab.setBackground(null);
    		break;
    		case KeyEvent.VK_SHIFT: lShift.setBackground(null);
    		rShift.setBackground(null);
    		break;
    		case KeyEvent.VK_CAPS_LOCK: caps.setBackground(null);
    		break;
    		default: break;
    	}}}
    	
    	
    	
    }

	@Override
	public void keyTyped(KeyEvent e) { //there's a bug with the program if i typed s instead of a and the next sentence was sentence and you didn't type the s then s becomes black
		//the total chars don't add up correctly ["Theq, uick, brown] for this the q in quick becomes dark and so does the b in brown
		//another example ["Theqq, uixk, brown, fox, null]
		//you'll see this once you type really fast
		/*
        if (e.getKeyCode() == KeyEvent.VK_BACK_SPACE && numOfWords > 0 && txtType.getText().isEmpty()) {
        	typedWords.remove(typedWords.size()-1);
    		numOfWords--; //this doesn't work
    		txtType.setText(typedWords.get(numOfWords));
    		currentChar = typedWords.get(numOfWords).length();
    		totalChars--; //space in between words
			
			if (typedWords.get(numOfWords).length() < correctWords[numOfWords].length()) {
				totalChars -= (correctWords[numOfWords].length() - typedWords.get(numOfWords).length()); 
				totalChars++; // both have to add by one since in keyTyped method these subtract by one
				currentChar++;
			}
        }
        */
		time.start();
		//backspace is pressed
		if (e.getKeyChar() == (KeyEvent.VK_BACK_SPACE) && totalChars > 0) { 
			
			//scenario 1, moving back to previous word
			//bug making an error sound 
			if (numOfWords > 0 && txtType.getText().isEmpty() && currentChar == 0) { //moving back to previous word
				typedWords.remove(typedWords.size()-1);
	    		numOfWords--; //this doesn't work
	    		txtType.setText(typedWords.get(numOfWords));
	    		currentChar = typedWords.get(numOfWords).length();
	    		totalChars--; //space in between words
	    		System.out.println(totalChars + correctWords[numOfWords].length());
				
	    		try {
					textPane.getHighlighter().removeAllHighlights();
					textPane.getHighlighter().addHighlight(totalChars - correctWords[numOfWords].length(), totalChars, highlightPainter);
				} catch (BadLocationException b) {
					
				}
				
				if (txtType.getText().length() < correctWords[numOfWords].length()) {
					System.out.println(totalChars);
					totalChars -= (correctWords[numOfWords].length() - typedWords.get(numOfWords).length()); 
					//totalChars++; // both have to add by one since in keyTyped method these subtract by one
					//currentChar++;
				}
					
			} //End of moving back to previous word
			
			//Scenario 2, deleting a char
			else if (txtType.getText().length() < correctWords[numOfWords].length()) { // < and not <= because once the backspace is typed then it will become one char smaller, therefore compare what's after backspace is pressed
				totalChars--; 
				currentChar--;
			} //if over the correct Word length then don't count it as subtraction from total amount of chars and current chars
			
			//Scenario 3, user typed correct words but too many chars if deletes the chars and length are now the same compare 
			else if (txtType.getText().length() == correctWords[numOfWords].length()) { //this loops through word to color the correct chars and incorrect ones
				
				totalChars -= correctWords[numOfWords].length();
				
				for (int i = 0; i < correctWords[numOfWords].length(); i++) {
					
			       
			        if (txtType.getText().charAt(i) != correctWords[numOfWords].charAt(i)) {
			        	doc.setCharacterAttributes(totalChars, 1, normal, true);
			        	System.out.println("why isn't this running"); 
			        }
			        	
			        
			        else if(txtType.getText().charAt(i) == correctWords[numOfWords].charAt(i))
			        {
			        	System.out.println(txtType.getText().charAt(i));
			        	System.out.println(correctWords[numOfWords].charAt(i));
			        	System.out.println(totalChars);
			        	System.out.println("why isn't this running"); 
			        	doc.setCharacterAttributes(totalChars, 1, correct, true); // not working
			        }
			        	 
					totalChars++; 
				}
			}
			
			doc.setCharacterAttributes(totalChars, 1, normal, true); 
			System.out.println("1.total:" + totalChars);
			System.out.println("2.current:" + currentChar);
		}
		
		
		//spacebar is pressed
		//else 
		if (e.getKeyChar() == (KeyEvent.VK_SPACE)) {
			
			System.out.println("typed word:" + txtType.getText());
			
			if (txtType.getText().length() < correctWords[numOfWords].length()) {
				totalChars+= correctWords[numOfWords].length() - txtType.getText().length();  //not working
			}

			totalChars++; //this is kept since the space adds a char in length
		
        	if (numOfWords == 0 && doneBefore == false) { //this is to check whether the user has typed the first word already, if so then set the first element, if not then add the first element
        		typedWords.add(txtType.getText().replaceAll(" ", ""));
        	    doneBefore = true;
        	}
        	
        	else 
        		typedWords.set(numOfWords, txtType.getText().replaceAll(" ", ""));

        	numOfWords++;
            typedWords.add(null);
            currentChar = 0;     

            	try {
					textPane.getHighlighter().removeAllHighlights();
					textPane.getHighlighter().addHighlight(totalChars, totalChars + correctWords[numOfWords].length(), 
					        highlightPainter);
				} catch (BadLocationException b) {
					
				}
				
		}
		
		//any char that is typed
		else {

			try {
				
			//correct chars
	        if (e.getKeyChar() == correctWords[numOfWords].charAt(currentChar) && e.getKeyChar() != (KeyEvent.VK_SPACE)) {
	        	doc.setCharacterAttributes(totalChars, 1, correct, true); 
	        	currentChar++;
	        	totalChars++;
	        }
	        //incorrect chars
	        else if (e.getKeyChar() != correctWords[numOfWords].charAt(currentChar) && e.getKeyChar() != (KeyEvent.VK_BACK_SPACE) && e.getKeyChar() != (KeyEvent.VK_SPACE)) {
	        	doc.setCharacterAttributes(totalChars, 1, incorrect, true); 
	        	currentChar++;
	        	totalChars++;
	        }
        	System.out.println("1.total:" + totalChars);
        	System.out.println("2.current:" + currentChar);
        	System.out.println("3.correct:" + correctWords[numOfWords].charAt(currentChar-1)); // this is different from typed sometimes
        	System.out.println("4.Typed:" + e.getKeyChar());
        	
        	calculateCPMWPM();
        	
			} catch(IndexOutOfBoundsException i) { //whole word becomes red
				doc.setCharacterAttributes(totalChars-correctWords[numOfWords].length(), correctWords[numOfWords].length(), incorrect, true); 
			}
		}
      
	}
	
	public void calculateCPMWPM() {
        double timeElapsed = System.nanoTime() - startTime;
        String words = typedWords.toString();
        int numOfChars = words.length();
        int cpm = (int) (numOfChars / (timeElapsed / 1000000000) * 60); 
        lblCPM.setText("CPM: " + cpm);
        lblWPM.setText("WPM: " + cpm/5);
    }
	
	public void highlight() {
		
	}

	public int getNetCPM() {
		String typedChars = "";
		for (int i = 0; i < typedWords.size()-1; i++)
			typedChars += typedWords.get(i);
		return typedChars.length();
	}
	
	public int getNetWPM() {
		String typedChars = "";
		for (int i = 0; i < typedWords.size()-1; i++)
			typedChars += typedWords.get(i);
		return typedChars.length()/5;
	}
	
	public int getCPM() {
		String typedChars = "";
		for (int i = 0; i < typedWords.size()-1; i++)
			typedChars += typedWords.get(i);
		
		for (int i = 0; i < typedChars.length(); i++) {
			if (typedChars.charAt(i) == text.replaceAll(" ", "").charAt(i)) 
				rightChar++;
		}
		
		return rightChar;
	}
	
	public int getWPM() {
		return rightChar/5;
	}
	
	public double getAccuracy() {
		String typedChars = "";
		for (int i = 0; i < typedWords.size()-1; i++)
			typedChars += typedWords.get(i);
		double accuracy = (rightChar/typedChars.length()) * 100;
		return accuracy;
	}
	
	public void importText() throws Exception{
		
		//www.youtube.com/watch?v=xkcs25Ustag
		
		JFileChooser fileChooser = new JFileChooser();
		 
		  
		  if(fileChooser.showOpenDialog(null) == JFileChooser.APPROVE_OPTION){
		   
		   //get the file
		   java.io.File file = fileChooser.getSelectedFile();
		   
		   //create a scanner for the file
		   Scanner input = new Scanner(file);
		   String sb = new String();
		   
		   //read text from file
		   while(input.hasNext()){
		    sb += input.nextLine();
		   }
		   
		   text = sb;
		   correctChars = text.toCharArray();
		   correctWords = text.split(" ");
		   textPane.setText(text);
		   input.close();
		   try {
	    		textPane.getHighlighter().removeAllHighlights();
				textPane.getHighlighter().addHighlight(0, correctWords[numOfWords].length(), 
				        highlightPainter);
			} catch (BadLocationException b) {
				
			}
		  }
		  else{
		   textPane.setText("No file was selected");
		  }
	}
} // end class

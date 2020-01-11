# Stacey-Du
import java.awt.BorderLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JCheckBox;
import javax.swing.JComboBox;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JRadioButton;
import javax.swing.JTextArea;
import javax.swing.border.EtchedBorder;
import javax.swing.border.TitledBorder;
import javax.swing.JFrame;
import javax.swing.JTextField;
import javax.swing.ButtonGroup;
import javax.swing.JScrollPane;

/**
   This frame is used to calculate adult's daily needed calories
   by knowing their weight, age and exercise type
 */
public class CalorieCalculatorFormFrame extends JFrame
{
    private static final int FRAME_WIDTH= 500;
    private static final int FRAME_HEIGHT=500;
  
    private JLabel resultLabel;
    private JLabel weightLabel;
    private JCheckBox swimCheckBox;
    private JCheckBox danceCheckBox;
    private JCheckBox yogaCheckBox;
    private JRadioButton maleButton;
    private JRadioButton femaleButton;
    private JComboBox ageCombo;
    private JTextField weightField;
    private JButton button;
    private ActionListener Listener;
    private double result= 0;
    private static final double DEFAULT_WEIGHT = 0;
    private JTextArea resultArea;
    private static final int AREA_ROWS = 10;
    private static final int AREA_COLUMNS = 25;
 
    /**
       Constructs the frame
    */
  
    public CalorieCalculatorFormFrame()
    {
	   // Create a panel for result area.  
           JPanel main = new JPanel();
	   add(main,BorderLayout.NORTH);
	
	   // Create a scrollable text area labelled "Results".
	   resultLabel = new JLabel("Results: ");
	   main.add(resultLabel);
	
	   resultArea= new JTextArea(AREA_ROWS, AREA_COLUMNS);
	   resultArea.setEditable(false);
	
	   JScrollPane scrollPane = new JScrollPane(resultArea);
	   main.add(scrollPane);
	
	   // Construct a menu bar.
	   JMenuBar menuBar = new JMenuBar();
	   setJMenuBar(menuBar);
	   menuBar.add(createFileMenu());
	
	   createControlPanel();
	   createButton();
	   setSize(FRAME_WIDTH, FRAME_HEIGHT);
    }
    
    /**
       This listener controls "Exit" in File menu to exit
     */
    class ExitItemListener implements ActionListener
    { 
    	public void actionPerformed(ActionEvent event)
	    {
	       System.exit(0) ;
	    }
    }
  
    /**
       This listener controls "Clear" in File menu to clear texts 
    */
    class ClearTextListener implements ActionListener
    { 
    	public void actionPerformed(ActionEvent event)
	    {
	       weightField.setText(""+ DEFAULT_WEIGHT);
	       resultArea.setText("");
	    }
    }
    
    /**
       Create File menu to let user implement clear and exit action
     */
    public JMenu createFileMenu()
    {
	  JMenu menu= new JMenu("File");
	  JMenuItem exitItem = new JMenuItem("Exit");
	  ActionListener listener1 = new ExitItemListener();
	  exitItem.addActionListener(listener1);
	  menu.add(exitItem);
	  
	  JMenuItem clearItem = new JMenuItem("Clear");
	  ActionListener listener2 = new ClearTextListener();
	  clearItem.addActionListener(listener2);
	  menu.add(clearItem);
	  return menu;
    }
  
    /**
       Create the control panel to organize all kinds of buttons
     */
    public void createControlPanel()
    {
	   JPanel weightPanel = createTextField();
	   JPanel genderGroupPanel = createRadioButtons();
	   JPanel ageGroupPanel = createComboBox();
	   JPanel exerciseGroupPanel = createCheckBox();
	   JPanel buttonPanel = createButton();
	  
	   JPanel controlPanel= new JPanel();
	   controlPanel.setLayout(new GridLayout(5,1));
	   controlPanel.add(weightPanel);
	   controlPanel.add(genderGroupPanel);
	   controlPanel.add(ageGroupPanel);
	   controlPanel.add(exerciseGroupPanel);
	   controlPanel.add(buttonPanel);
	  
	   // Add panels to content pane
	   
	   add(controlPanel,BorderLayout.SOUTH);
    }
  
    /**
        Create a text field to input the weight of user
        @return the panel containing text field
    */
    public JPanel createTextField()
    {
	   weightLabel = new JLabel("Please Enter Your Weight(kg):");
		  
	   final int FIELD_WIDTH = 20;
	   weightField = new JTextField(FIELD_WIDTH);
	   weightField.setText(""+ DEFAULT_WEIGHT);
		  
	   JPanel panel = new JPanel();
	   panel.add(weightLabel);
	   panel.add(weightField);
		  
	   return panel;
    }
  
    /**
       Create the radio buttons to select gender
       @return the panel containing the radio buttons
     */
    public JPanel createRadioButtons()
    {
	   maleButton = new JRadioButton("Male");
	   maleButton.addActionListener(Listener);
		  
	   femaleButton = new JRadioButton("Female");
	   femaleButton.addActionListener(Listener);
	   maleButton.setSelected(true);
	   
	   // Add radio buttons to button group
	   
	   ButtonGroup group = new ButtonGroup();
	   group.add(maleButton);
	   group.add(femaleButton);
				 
	   JPanel panel = new JPanel();
	   panel.add(maleButton);
	   panel.add(femaleButton);
	   panel.setBorder(new TitledBorder(new EtchedBorder(), "Gender"));
		  
	   return panel;
    }
	  
    /**
       Create the combo box with age ranges
       @return the panel containing the combo box
    */
    public JPanel createComboBox()
	{
	   ageCombo = new JComboBox();
	   ageCombo.addItem("age is from 18 to 30");
	   ageCombo.addItem("age from 31 to 60");
	   ageCombo.addItem("older than 60");
	   ageCombo.setEditable(false);
	   ageCombo.addActionListener(Listener);
		  
	   JPanel panel = new JPanel();
	   panel.add(ageCombo);
	   
	   return panel;
    }	  
	  
    /**
       Create the check boxes for selecting exercises user want
       @return the panel containing the check boxes
    */
    public JPanel createCheckBox()
    {
	   swimCheckBox = new JCheckBox("Swim");
	   swimCheckBox.addActionListener(Listener);
		  
	   danceCheckBox = new JCheckBox("Dance");
       danceCheckBox.addActionListener(Listener);
		  
	   yogaCheckBox = new JCheckBox("Yoga");
	   yogaCheckBox.addActionListener(Listener);
		  
	   JPanel panel = new JPanel();
	   panel.add(swimCheckBox);
	   panel.add(danceCheckBox);
	   panel.add(yogaCheckBox);
	   panel.setBorder(new TitledBorder(new EtchedBorder(),"One Hour Exercise"));
		  
	   return panel;
    }
   
    /**
       Create "Done" button to generate the conditions and calculate result
       @return the panel containing the button
    */
    private JPanel createButton()
    {  
           // This listener gets selected conditions for calculation.
    	
        class DoneListener implements ActionListener
        {
	      public void actionPerformed(ActionEvent event)
	      {
		 // Get age range
		 String age = (String)ageCombo.getSelectedItem();
		      
		 // Get weight
		 double weight = Double.parseDouble(weightField.getText());
			  
		 // Calculate the result with conditions of age and gender
		 if(age.equalsIgnoreCase("age is from 18 to 30")) 
	         {
		     if(maleButton.isSelected())
		     {result= 15.2 * weight + 680;}
		     else if(femaleButton.isSelected()) 
		     {result= 14.6 * weight + 450;}
	         }
		 else if(age.equalsIgnoreCase("age from 31 to 60")) 
	         { 
	             if(maleButton.isSelected())
		     {result= 11.5 * weight + 830;}
		     else if (femaleButton.isSelected())
		     {result= 8.6 * weight + 830;}
		 }
	         else if (age.equalsIgnoreCase("older than 60")) 
	         {
		     if(maleButton.isSelected())
		     {result= 13.4 * weight + 490;}
	             else if ( femaleButton.isSelected())
		     {result= 10.4 * weight + 600;}
		 }
			  
		 // Add extra needed calories for choosing wanted exercises
                 if (swimCheckBox.isSelected())
	         {result = result + 497;}
	         if (danceCheckBox.isSelected())
	         {result = result + 452;}
	         if (yogaCheckBox.isSelected())
		 {result = result + 180;}  
			  
		 //Present the result
	         resultArea.setText("As an adult, the daily calories you need are about:"+Double.toString(result)+"  kilocalorie.");
			  
                 } 
         }
	  
          // Create button and set its location
          button = new JButton ("Done");
	  ActionListener listener = new DoneListener();
	  button.addActionListener(listener);
	  JPanel panel = new JPanel();
	  panel.add(button);
		  
		  return panel;
    }
} 		  

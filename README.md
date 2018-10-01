# personal_project
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package receptionist;

/**
 *
 * @author julie
 */
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.*;
import java.util.logging.Level;
import java.util.logging.Logger;

public  class Receptonist extends JFrame implements ActionListener{
    
 Container container=getContentPane();
 JLabel UsernameLabel=new JLabel("Username");
 JLabel PasswordLabel=new JLabel("Password");
 JTextField UsernameTextField=new JTextField ();
 JPasswordField PasswordField=new JPasswordField ();
 JButton ClearButton=new JButton("CLEAR");
 JButton LoginButton=new JButton("LOGIN");
 JCheckBox showPassword=new JCheckBox("Show password");
 
 Receptonist (){
     setLayoutManager();
     setLocationAndSize();
     addComponenetsToContainer();
     addActionEvent();
 }
 public final void setLayoutManager(){
     container.setLayout(null);
 }
 private void setLocationAndSize(){
     UsernameLabel.setBounds(50,150,100,30);
     PasswordLabel.setBounds(50,220,100,30);
     UsernameTextField.setBounds(150,150,150,30);
     PasswordField.setBounds(150,220,150,30);
     showPassword.setBounds(150,250,150,30);
     ClearButton.setBounds(50,300,100,30);
     LoginButton.setBounds(200,300,100,30); 
 }
 public void addComponentsToContainer(){
     container.add(UsernameLabel);
     container.add(PasswordLabel);
     container.add(UsernameTextField);
     container.add(PasswordField);
     container.add(showPassword);
     container.add(ClearButton);
     container.add(LoginButton);
 }
 private void addActionEvent(){
     ClearButton.addActionListener(this);
     LoginButton.addActionListener(this);
     showPassword.addActionListener(this);
 }
 @Override
 public void actionPerformed(ActionEvent e){
     if(e.getSource()==LoginButton){
         String UsernameText;
         String pwdText;
         UsernameText= UsernameTextField.getText();
         pwdText= PasswordField.getText();
         if(UsernameText.equalsIgnoreCase("Frontdesk")&&pwdText.equalsIgnoreCase("234Java")){
           JOptionPane.showMessageDialog(this,"Login succesful");  
         }
         else{
         JOptionPane.showMessageDialog(this,"Invaild username or password"); 
     }
     }
 
 
   if(e.getSource()==ClearButton);{
       UsernameTextField.setText("");
       PasswordField.setText("");
     
 }

   if(e.getSource()==showPassword)
   {
       if(showPassword.isSelected()){
           PasswordField.setEchoChar((char)0);
       }
       else{
           PasswordField.setEchoChar('*');
       }
   }
   }
    private void addComponenetsToContainer() {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
    
     public static void main(String[] args){
         JFrame myframe=new JFrame("Receptionist");
         myframe.setBounds(10,10,370,600);
         myframe.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         myframe.setResizable(false);
         myframe.setVisible(true);
     }
 }
public class Receptionist{
    private Connection conn;
    private Statement st;
    private ResultSet rs;
    
    public Receptionist() throws SQLException{
        
 try{
     
    Class.forName("com.mysql.jbdc.Driver");
            
           conn=DriverManager.getConnection("jbdc:mysql://localhost/OOPclass", "root","");
        System.out.println("Connection Established...");
        
        Statement stm=conn.createStatement();
        
        String query1="INSERT INTO LOGIN VALUES('Username','Password')";
        stm.executeUpdate(query1);
        System.out.println("Query 1 success");
        
        String query2 ="SELECT * FROM LOGIN";
        rs=stm.executeQuery(query2);
        while(rs.next()){
            String Username=rs.getString("Username");
            String Password=rs.getString("Password");
            
            System.out.println("Username:"+Username+"Password:"+Password);
        }
        System.out.println("Results obtained");
        
    catch(Exeption e){
            System.out.println("Error");
            }
}       catch (ClassNotFoundException ex) {
            Logger.getLogger(Receptionist.class.getName()).log(Level.SEVERE, null, ex);
        }
}
}

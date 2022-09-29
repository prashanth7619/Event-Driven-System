package calculatorgui;
import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.GridLayout;
import java.awt.Panel;
import java.awt.TextField;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;
public class CalculatorGui extends WindowAdapter implements ActionListener{
Button button[] = new Button[17];
TextField textDisplay;
String operand;
public String num="",num1="",num2="";
public CalculatorGui() {
Frame frame= new Frame("Calculator");
textDisplay = new TextField(30);
frame.setLayout(new FlowLayout());
Panel textPanel = new Panel();
textPanel.add(textDisplay);
frame.add(textPanel);
Panel buttonPanel = new Panel();
buttonPanel.setLayout(new GridLayout(4, 4, 2, 2));
for(int i=0;i<=9;i++){
button[i]=new Button(i+"");
}
button[10]=new Button("+");
button[11]=new Button("-");
button[12]=new Button("*");
button[13]=new Button("/");
button[14]=new Button("%");
button[15]=new Button("=");
button[16]=new Button("C");
for(int i=0;i<17;i++)
buttonPanel.add(button[i]);
for(int i=0;i<17;i++)
button[i].addActionListener(this);
frame.add(buttonPanel);
frame.setSize(350,350);
frame.setVisible(true);
}

public static void main(String[] args) {
new CalculatorGui();
}
public double calc(String op,double num1, double num2){
double res=0;
switch(op){
case "+": res=num1+num2;
break;
case "-": res=num1-num2;
break;
case "*": res=num1*num2;
break;
case "/": res=num1/num2;
break;
}
return res;
}
@Override
public void actionPerformed(ActionEvent ae) {
double res=0;
String key = ae.getActionCommand();
if(key.equals("0")|key.equals("1")|key.equals("2")|key.equals("3")
| key.equals("4")|key.equals("5")|key.equals("6")|
key.equals("7")|key.equals("8")|key.equals("9"))
{
num+=key;
textDisplay.setText(num);
}
else if(key.equals("+")|key.equals("-")|key.equals("*")|key.equals("/")){
operand = key;
if(!num.equals("")){
num1 = num;
textDisplay.setText("");
num="";
}
else{
textDisplay.setText("error");
}
}
else if(key.equals("=")){
num2=num;
try{
if(!num1.equals("")&& !num2.equals("")){
res = calc(operand,Double.parseDouble(num1),Double.parseDouble(num2));
}
}catch(NumberFormatException nfe){
}
num2 = res+"";
num=num2;
num1=num2;
textDisplay.setText(num1+"");
}
else if(key.equals("C")){

textDisplay.setText("");
num=num1=num2="";
}
}
@Override
public void windowClosing(WindowEvent arg0) {
System.exit(0);
}
}

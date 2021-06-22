package sample;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.TextArea;
import javafx.scene.control.TextField;

public class Controller {
    private String strTemp="";

    @FXML
    private TextArea text1;

    @FXML
    private TextArea text2;

    @FXML
    private TextField text_key;

    @FXML
    void decrypt_press(ActionEvent event) {
        int varForMod;
        int key = Integer.parseInt(text_key.getText());
        if(key>25)
            key%=26;
        for(int i=0; i<text1.getLength(); i++) {
            if((text1.getText().charAt(i)>64 && text1.getText().charAt(i)<91) || (text1.getText().charAt(i)>96 && text1.getText().charAt(i)<123)) {
                if(((text1.getText().charAt(i) - key) < 97) && ((text1.getText().charAt(i)) > 96)) {
                    varForMod =123- (97 - (text1.getText().charAt(i)-key));
                    strTemp+=(char)(varForMod);
                }
                else if(((text1.getText().charAt(i)) > 64 && ((text1.getText().charAt(i) - key) < 65))) {
                    varForMod=91-(65 - (text1.getText().charAt(i)-key));
                    strTemp+=(char)(varForMod);
                }
                else {
                    strTemp += (char) (text1.getText().charAt(i) - key);
                }
            }
            else {
                strTemp+=text1.getText().charAt(i);
            }
        }
        text2.setText(strTemp);
        strTemp="";
    }

    @FXML
    void encrypt_press(ActionEvent event) {
        int varForMod;
        int key = Integer.parseInt(text_key.getText());
        if(key>25)
            key%=26;
        for(int i=0; i<text1.getLength(); i++) {
            if((text1.getText().charAt(i)>64 && text1.getText().charAt(i)<91) || (text1.getText().charAt(i)>96 && text1.getText().charAt(i)<123)) {
                if((text1.getText().charAt(i) + key) > 122) {
                    varForMod=(text1.getText().charAt(i) + key - 96)%26;
                    strTemp+=(char)(96+(varForMod));
                }
                else if(((text1.getText().charAt(i)) < 91 && ((text1.getText().charAt(i) + key) > 90))) {
                    varForMod=(text1.getText().charAt(i) + key - 64)%26;
                    strTemp+=(char)(64+varForMod);
                }
                else {
                    strTemp += (char) (text1.getText().charAt(i) + key);
                }
            }
            else {
                strTemp+=text1.getText().charAt(i);
            }
        }
        text2.setText(strTemp);
        strTemp="";
    }

}

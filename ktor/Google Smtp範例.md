# How to use gmail account to push smtp mail !!

###  1.Add in gradle

```kotlin
implementation group: 'javax.mail', name: 'mail', version: '1.4.1'
```

### 2.Sample Class
```kotlin
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.text.SimpleDateFormat;
import java.util.*;
import javax.activation.*;
import java.util.Properties;
import javax.mail.Message;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
public class ses {

    // Replace sender@example.com with your "From" address.
    // This address must be verified.
    static final String FROM = "sample@squarestudio.com";
    static final String FROMNAME = "T-sport體育平台";
    // Replace smtp_username with your Amazon SES SMTP user name.
    static final String SMTP_USERNAME = "sampleMail";
    // Replace smtp_password with your Amazon SES SMTP password.
    static final String SMTP_PASSWORD = "samplePassword";
    // The name of the Configuration Set to use for this message.
    // If you comment out or remove this variable, you will also need to
    // comment out or remove the header below.
    static final String CONFIGSET = "ss";
    // Google SES SMTP host name. This example uses the 美國西部 (奧勒岡) region.
    static final String HOST = "smtp.gmail.com";
    // The port you will connect to on the Google SES SMTP endpoint.
    static final int PORT = 465;

    public static void getMessage(){
        try
        {
            String BODY=String.join(
                    System.getProperty("line.separator"),"Hello Smtp");
            Properties props = System.getProperties();
            props.put("mail.transport.protocol", "smtp");
            props.put("mail.smtp.port", PORT);
            props.put("mail.smtp.starttls.enable", "true");
            props.put("mail.smtp.auth", "true");
            // Create a Session object to represent a mail session with the specified properties.
            Session session = Session.getDefaultInstance(props);
            // Create a message with the specified information.
            ArrayList<MimeMessage> allmsg=new ArrayList<MimeMessage>();
            String[] user=new String[]{"sam38124@gmail.com"};
//        String[] user=new String[]{"jianzhi.wang@orange-electronic.com"};
            for(String use:user){
                MimeMessage msg = new MimeMessage(session);
                msg.setFrom(new InternetAddress(FROM,FROMNAME));
                msg.setRecipient(Message.RecipientType.TO, new InternetAddress(use));
                msg.setSubject("Mail title");
                msg.setContent(BODY,"text/html");
                msg.setHeader("X-SES-CONFIGURATION-SET", CONFIGSET);
                allmsg.add(msg);
            }
            // Create a transport.
            Transport transport = session.getTransport();
            // Send the message.
            System.out.println("Sending...");
            // Connect to Amazon SES using the SMTP username and password you specified above.
            transport.connect(HOST, SMTP_USERNAME, SMTP_PASSWORD);
            // Send the email.
            for(MimeMessage i:allmsg){
                transport.sendMessage(i, i.getAllRecipients());
            }
            System.out.println("Email sent!");
            transport.close();
        }
        catch (Exception ex) {
            ex.printStackTrace();
            System.out.println("The email was not sent.");
            System.out.println("Error message: " + ex.getMessage());
        }
    }
    public static void main(String[] args) throws Exception {
        getMessage();
    }

}
```

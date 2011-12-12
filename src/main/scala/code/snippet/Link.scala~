package code
package snippet

import model._
import comet._
import lib._

import net.liftweb._
import http._
import util.Helpers._
import js._
import JsCmds._
import js.jquery.JqJsCmds._

import javax.mail._
import javax.mail.internet._
import java.util.Properties._

class Link {
  // open a modal dialog based on the _share_link.html template
  def request = "* [onclick]" #> SHtml.ajaxInvoke(() => {
    (for {
      template <- TemplateFinder.findAnyTemplate(List("_share_link"))
    } yield ModalDialog(template)) openOr Noop
      
  })

  // close the modal dialog
  def close = "* [onclick]" #> SHtml.ajaxInvoke(() => Unblock)

  // Generate the href and link for sharing
  def generate = {
    val s = ShareCart.generateLink(TheCart)
    "a [href]" #> s & "a *" #> s
  }

  def send = "* [onclick]" #> SHtml.ajaxInvoke(() => {
	//print("hello world")
	// Get the user's message
	var bodyText = "Hello"
	val host = "smtp.gmail.com"
	val port = 587
	val username = "srikanth4wipro"
	val password = "nivedinee"



	// Set up the mail object
	val props = System.getProperties
	props.put("mail.smtp.host", "smtp.gmail.com");
	props.put("mail.smtp.socketFactory.port", "465");
	props.put("mail.smtp.socketFactory.class",
			"javax.net.ssl.SSLSocketFactory");
	props.put("mail.smtp.auth", "true");
	props.put("mail.smtp.port", "465");	  

	val session = Session.getDefaultInstance(props,
		new javax.mail.Authenticator() {
    override def getPasswordAuthentication = new PasswordAuthentication(username, password)
 })
	
	val message = new MimeMessage(session)

	// Set the from, to, subject, body text
	message.setFrom(new InternetAddress("srikanth4wipro@gmail.com"))
	message.setRecipients(Message.RecipientType.TO, "srikanth.1.kyatham@gmail.com")
	message.setSubject("Greetings from langref.org")
	message.setText(bodyText)

	// And send it
	val transport = session.getTransport("smtp");
	transport.connect(host, port, username, password);
	Transport.send(message)
	//System.out.println("Done"); 
	Unblock
  })

}

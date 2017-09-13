package calendar;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.text.SimpleDateFormat;
import java.util.Date;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/CreateEvent")
public class CreateEvent extends HttpServlet {
   private static final long serialVersionUID = 1L;
   static String             url              = "jdbc:mysql://swe-mitchellhuston.ddns.net:3306/calendar_db";
   static String             user             = "mitchellhuston-remote";
   static String             password         = "password";
   static Connection         connection       = null;

   public CreateEvent() {
      super();
   }

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
      response.setContentType("text/html;charset=UTF-8");
      
      connection = null;
      
      String username = null;
      String eventName = null;
      Date date = null;
      String eventLocation = null;
      
      try {
    	  username = request.getParameter("username");
    	  eventName = request.getParameter("eventName");
    	  date = new SimpleDateFormat("MM/dd/yyyy").parse(request.getParameter("date"));
    	  eventLocation = request.getParameter("eventLocation");
      } catch(Exception e) {
    	 response.getWriter().println("Failed to retrieve event creation data.<br>");
      }
      
      try {
         connection = DriverManager.getConnection(url, user, password);
      } catch (SQLException e) {
    	 response.getWriter().println("Failed to make connection.<br>");
         return;
      }
      if (connection != null) {
         
      } else {
    	 response.getWriter().println("Failed to make connection.<br>");
    	 return;
      }
      try {
         String insertSQL = "INSERT INTO Events (username, eventName, date, eventLocation) VALUES (?, ?, ?, ?)";
         PreparedStatement insertNewEvent = connection.prepareStatement(insertSQL);
         
         insertNewEvent.setString(1, username);
         insertNewEvent.setString(2, eventName);
         insertNewEvent.setDate(3, new java.sql.Date(date.getTime()));
         insertNewEvent.setString(4, eventLocation);
         
         insertNewEvent.executeUpdate();
      } catch (SQLException e) {
    	 response.getWriter().println("Failed while inserting new event to database.<br>");
    	 e.printStackTrace();
    	 return;
      }
      try { 
    	  response.getWriter().append("Successfully created new event.<br><br>");

          response.getWriter().append("Username: " + username + "<br>");
          response.getWriter().append("Event Name: " + eventName + "<br>");
          response.getWriter().append("Event Date: " + date + "<br>");
          response.getWriter().append("Event Location: " + eventLocation + "<br><br>");
      } catch (Exception e) { 
    	  response.getWriter().println("Failed while listing new event (Creation process still succeeded?)");
    	  return;
      }
   }

   protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
      doGet(request, response);
   }
}
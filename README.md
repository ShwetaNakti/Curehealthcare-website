# Curehealthcare-website
// Automation script for testing 
package Database_project;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.Select;

public class Doc_db {

	public static void main(String[] args) throws SQLException, Exception  {
		// TODO Auto-generated method stub

		//browser address
		System.setProperty("webdriver.chrome.driver","C:\\Users\\Shweta\\OneDrive\\Desktop\\chromedriver-win64\\chromedriver.exe");
		
		//open Browser
		WebDriver driver = new ChromeDriver();
		
		//maximize window
		driver.manage().window().maximize();

		//connecting to database
		Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/shweta", "root", "admin");
		
		Statement stmt = con.createStatement();
		
		ResultSet rs = stmt.executeQuery("select * from doct;");
		
		while(rs.next()==true)
		{
			String id = rs.getString("Username");
			String pd = rs.getString("Password");
			System.out.println(pd);
			System.out.println(id);
			
			//browser url
			driver.get("https://katalon-demo-cura.herokuapp.com/profile.php#login");
			
			//locator for login
			driver.findElement(By.id("txt-username")).sendKeys(id);
			driver.findElement(By.id("txt-password")).sendKeys(pd);
			driver.findElement(By.xpath("//button[@id='btn-login']")).click();
			
			//Select dropdown
			Select s1 = new Select(driver.findElement(By.id("combo_facility")));
			s1.selectByIndex(2);
			Thread.sleep(1000);
			
			//select radio button
			driver.findElement(By.id("radio_program_medicaid")).click();
			Thread.sleep(1000);
			
			//select textbox
			WebElement cb1 = driver.findElement(By.name("hospital_readmission"));
			cb1.click();
			Thread.sleep(1000);
			
			//calender
			driver.findElement(By.id("txt_visit_date")).click();
			
			//select month
			WebElement month = driver.findElement(By.xpath("//body[1]/div[1]/div[1]/table[1]/thead[1]/tr[2]/th[3]"));
			month.click();
			
			//select date
			WebElement date = driver.findElement(By.xpath("//tbody/tr[1]/td[4]"));
			date.click();
			
			//comment
			driver.findElement(By.id("txt_comment")).sendKeys("Book Appointment...");
			
			Thread.sleep(2000);
			
			//click book appointment button
			driver.findElement(By.xpath("//button[@id='btn-book-appointment']")).click();
			
			//menu
			driver.findElement(By.xpath("//body/a[@id='menu-toggle']/i[1]")).click();
			
			//select profile
			driver.findElement(By.xpath("//a[contains(text(),'Profile')]")).click();
			
			Thread.sleep(2000);
			
			//logout
			driver.findElement(By.linkText("Logout")).click();
			
			
			
			
			
			
			
			
			
		}
	}

}

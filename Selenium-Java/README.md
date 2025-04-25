package selenium.tests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class LoginBankTest {

    WebDriver driver;

    @BeforeTest
    public void setUp() {
        // Set the path of the ChromeDriver (you need to download ChromeDriver)
        System.setProperty("webdriver.chrome.driver", "path_to_chromedriver");

        // Initialize the ChromeDriver
        driver = new ChromeDriver();

        // Open the banking login page
        driver.get("https://www.examplebank.com/login");
    }

    @Test
    public void testLogin() {
        // Find the username, password fields, and login button
        WebElement usernameField = driver.findElement(By.id("username"));
        WebElement passwordField = driver.findElement(By.id("password"));
        WebElement loginButton = driver.findElement(By.id("loginButton"));

        // Enter valid credentials
        usernameField.sendKeys("valid_username");
        passwordField.sendKeys("valid_password");

        // Click the login button
        loginButton.click();

        // Wait for page to load and check if the user is redirected to the dashboard
        String expectedTitle = "Bank Dashboard";
        String actualTitle = driver.getTitle();
        
        // Assert that the login was successful
        Assert.assertEquals(actualTitle, expectedTitle, "Login failed or wrong page title!");
    }

    // Close the browser after the test
    @AfterTest
    public void tearDown() {
        driver.quit();
    }
}


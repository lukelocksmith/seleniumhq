// NuGet: Selenium.WebDriver.IEDriver
// NuGet: Selenium.WebDriver.ChromeDriver
// NuGet: Selenium.Mozilla.Firefox.Webdriver
// NuGet: Selenium.WebDriver.PhantomJS
using OpenQA.Selenium.Chrome;
using OpenQA.Selenium.Firefox;
using OpenQA.Selenium.PhantomJS;
using OpenQA.Selenium.IE;
IWebDriver driver = new ChromeDriver();
IWebDriver driver = new FirefoxDriver();
IWebDriver driver = new PhantomJSDriver();
IWebDriver driver = new InternetExplorerDriver();


IWebDriver Locator 

driver.FindElement(By.ClassName("className"));
driver.FindElement(By.CssSelector("css"));
driver.FindElement(By.Id("id"));
driver.FindElement(By.LinkText("text"));
driver.FindElement(By.Name("name"));
driver.FindElement(By.PartialLinkText("pText"));
driver.FindElement(By.TagName("input"));
driver.FindElement(By.XPath("//*[@id='editor']"));
// Find multiple elements
IReadOnlyCollection<IWebElement> anchors =
driver.FindElements(By.TagName("a"));
// Search for an element inside another
var element = driver.FindElement(By.TagName("div")).FindElement(By.TagName("a"));

ChromeDriver Locator

driver.FindElementByClassName("className");
driver.FindElementByCssSelector("css");
driver.FindElementById("someId");
driver.FindElementByName("nameAttribute");
driver.FindElementByLinkText("linkText");
driver.FindElementByPartialLinkText("partialText");
driver.FindElementByTagName("button");
driver.FindElementByXPath("//*[@id='someId']");
// same logic applied for FindElemens[…]

Basic Browser Operations
// Navigate to a page
driver.Navigate().GoToUrl(@"http://google.com");
driver.Url = @"http://google.com";
// Get the title of the page
string title = this.driver.Title;
// Get the current URL
string url = this.driver.Url;
// Get the current page HTML source
string html = this.driver.PageSource;

Page Navigate And Widnow Manage 
driver.Navigate().Back();
driver.Navigate().Forward();
driver.Navigate().Refresh();
driver.Manage().Window.FullScreen();
driver.Manage().Window.Minimize();
driver.Manage().Window.Maximize();

Basic Elements Operations

element.Click();
element.SendKeys("someText");
element.Clear();
element.Submit();
string innerText = element.Text;
bool isEnabled = element.Enabled;
bool isDisplayed = element.Displayed;
bool isSelected = element.Selected;

Basci Dropdown Operations

SelectElement select = new SelectElement(element);
select.SelectByIndex(1);
select.SelectByText("Ford");
select.SelectByValue("ford");
select.DeselectAll();
select.DeselectByIndex(1);
select.DeselectByText("Ford");
select.DeselectByValue("ford");
IWebElement selectedOption = select.SelectedOption;
IList<IWebElement> allSelected = select.AllSelectedOptions;
bool isMultipleSelect = select.IsMultiple;


Advanced Element Operations

// Drag and Drop
draggable = driver.FindElement(By.Id("draggable"));
drop = driver.FindElement(By.Id("droppable"));
new Actions(driver).DragAndDrop(draggable, drop).Perform();
new Actions(driver).DragAndDropToOffset(draggable, 30, 0).Perform();
new Actions(driver).ClickAndHold(draggable).MoveToElement(drop).Release().Perform();

// How to check if an element is visible
driver.FindElement(By.XPath("//*[@id='tve_editor']/div")).Displayed;
// Upload a file 
element.SendKeys(@"C:\UploadFile.png");
// Scroll to element
var element = driver.FindElement(By.Id("someId"));
 ((IJavaScriptExecutor)driver).ExecuteScript("arguments[0].scrollIntoView({block: 'center'})", element) 
// View  Screenshot, 
var screenshot = ((ITakesScreenshot)driver).GetScreenshot();
screenshot.SaveAsFile("filename", ImageFormat.Png);
// Element Screenshot
var element = driver.FindElement(By.XPath("//*[@id=someId]"));
var cropArea = new Rectangle(element.Location, element.Size);
var bitmap = bmpScreen.Clone(cropArea, bmpScreen.PixelFormat);
bitmap.Save(fileName);
// Wait for visibility of an element
var wait = new WebDriverWait(driver, TimeSpan.FromSeconds(30));
wait.Until(ExpectedConditions.VisibilityOfAllElementsLocatedBy(By.Id("someId’)));
// Element Focus:
element.SendKeys(string.Empty);
 ((IJavaScriptExecutor)driver).ExecuteScript("arguments[0].focus();",element);

Advanced Wait Operations

// Implicit wait
driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(10);
// Asynchronous Js, could be useful with AJAX 
driver.Manage().Timeouts().AsynchronousJavaScript = TimeSpan.FromSeconds(10);
// Create object instance and pass default timeout
WebDriverWait webDriverWait = new WebDriverWait(driver, TimeSpan.FromSeconds(10));
// Interval between iteration
webDriverWait.PollingInterval = TimeSpan.FromMilliseconds(500);
// Ignore exceptions of type
webDriverWait.IgnoreExceptionTypes(typeof(ElementClickInterceptedException), typeof(NullReferenceException));
// Override default timeout
webDriverWait.Timeout = TimeSpan.FromSeconds(15);
// Condition
webDriverWait.Until(ExpectedConditions.ElementToBeClickable(By.XPath("//*[@id='someId']")));
// Custom condition
webDriverWait.Until(driver => driver.FindElement(By.XPath("//*[@id='someId']")).Text != null);
// Complex condition
webDriverWait.Until(driver =>
{
    bool result = driver.FindElement(By.XPath("//*[@id='someId']")).Text != null;
    return result;
} );
		

Advanced Browser Operations

// Handle JavaScript pop-ups
IAlert a = driver.SwitchTo().Alert();
a.Accept();
a.Dismiss();
// Switch between browser windows or tabs
ReadOnlyCollection<string> windowHandles = driver.WindowHandles;
string firstTab = windowHandles.First();
string lastTab = windowHandles.Last();
driver.SwitchTo().Window(lastTab);
// Add a new cookie
Cookie cookie = new OpenQA.Selenium.Cookie("key", "value");
this.driver.Manage().Cookies.AddCookie(cookie);
// Get all cookies
var cookies = this.driver.Manage().Cookies.AllCookies;
// Delete a cookie by name
this.driver.Manage().Cookies.DeleteCookieNamed("CookieName");
// Delete all cookies
this.driver.Manage().Cookies.DeleteAllCookies();
// Wait until a page is fully loaded via JavaScript
WebDriverWait wait = new WebDriverWait(this.driver, TimeSpan.FromSeconds(30));
wait.Until((x) =>
{
 return ((IJavaScriptExecutor)this.driver).ExecuteScript( "return document.readyState").Equals("complete");
});
// Switch to frames
this.driver.SwitchTo().Frame(1);
this.driver.SwitchTo().Frame("frameName");
IWebElement element = this.driver.FindElement(By.Id("id"));
this.driver.SwitchTo().Frame(element);
// Switch to the default document
this.driver.SwitchTo().DefaultContent();


Advanced Browser Configurations

// Set a HTTP proxy Firefox
FirefoxProfile firefoxProfile = new FirefoxProfile();
firefoxProfile.SetPreference("network.proxy.type", 1);
firefoxProfile.SetPreference("network.proxy.http", "myproxy.com");
firefoxProfile.SetPreference("network.proxy.http_port", 3239);
IWebDriver driver = new FirefoxDriver(firefoxProfile);
// Set a HTTP proxy Chrome
ChromeOptions options = new ChromeOptions();
var proxy = new Proxy();
proxy.Kind = ProxyKind.Manual;
proxy.IsAutoDetect = false;
proxy.HttpProxy =
proxy.SslProxy = "127.0.0.1:3239";
options.Proxy = proxy;
options.AddArgument("ignore-certificate-errors");
IWebDriver driver = new ChromeDriver(options);
// Accept all certificates Chrome
DesiredCapabilities capability = DesiredCapabilities.Chrome();
capability.SetCapability(CapabilityType.AcceptSslCertificates,true);
IWebDriver driver = new RemoteWebDriver(capability);
// Set Chrome options.
ChromeOptions options = new ChromeOptions();
DesiredCapabilities dc = DesiredCapabilities.Chrome();
dc.SetCapability(ChromeOptions.Capability, options);
IWebDriver driver = new RemoteWebDriver(dc);
// Turn off the JavaScript Firefox
FirefoxProfileManager profileManager = new FirefoxProfileManager();
FirefoxProfile profile = profileManager.GetProfile("HARDDISKUSER");
profile.SetPreference("javascript.enabled", false);
IWebDriver driver = new FirefoxDriver(profile);
// Set the default page load timeout
driver.Manage().Timeouts().SetPageLoadTimeout(new TimeSpan(10));
// Start Firefox with plugins
FirefoxProfile profile = new FirefoxProfile();
profile.AddExtension(@"C:\extensionsLocation\extension.xpi");
IWebDriver driver = new FirefoxDriver(profile);
// Start Chrome with a packed extension
ChromeOptions options = new ChromeOptions();
options.AddExtension(@"C:\extensions\extension_4_8_4_0.crx");
var driver = new ChromeDriver(options);
// Change the default files’ save location
ChromeOptions options = new ChromeOptions();
options.AddUserProfilePreference("download.default_directory", (@"C:\Download\");
var driver = new ChromeDriver(options);
// headless execution
options.AddArguments("--headless");
options.AddArguments("--disable-gpu");
// Disable info-bar
options.AddExcludedArgument("enable-automation");
 options.AddAdditionalCapability("useAutomationExtension", false);
// Browser Log
var service = ChromeDriverService.CreateDefaultService();
service.LogPath = LogFilePath;
service.EnableVerboseLogging = true;
var options = new ChromeOptions();
options.SetLoggingPreference(LogType.Browser, LogLevel.All);
this.Driver = new ChromeDriver(service, options);
// Chrome Emulation Mode
var emulationDevice = new ChromeMobileEmulationDeviceSettings();
emulationDevice.UserAgent = 
    "Mozilla/5.0 (iPhone;" +
    "CPU Nexus 6 like " +
    "Win64; x64)" +
    "AppleWebKit/536.26 (KHTML, like Gecko) " +
    "Version/6.0 " +
    "Mobile/10A5376e ";
emulationDevice.PixelRatio = 1.0;
var chromeOptions = new ChromeOptions();
chromeOptions.EnableMobileEmulation(emulationDevice);
var chromeDriver = new ChromeDriver(chromeOptions);

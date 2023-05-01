# Sdet-Architect

# Table of Contents
1. [Purpose](#purpose)
2. [Quality in the Context of Automated Software Testing](#quality-in-the-context-of-automated-software-testing)
3. [Overall Methodology in Testing Automation Structure](#overall-methodology-in-testing-automation-structure)
   1. [Test Scripts](#test-scripts)
   2. [Step Definitions](#step-definitions)
   3. [Application Control](#application-control)
   4. [External Dependencies](#external-dependencies)
4. [Web Application Testing](#web-application-software-automation)
   1. [Tool choice for Webdriver Automation](#tool-choice-for-webdriver-automation)
      1. [Free Tool: Selenium](#free-tool--selenium)
      2. [Paid Tool: Cyrpess](#paid-tool--cypress)
   2. [Example Projects](#example-web-automation-projects)
5. [Mobile Testing](#mobile-and-smart-device-automation)
   1. [Appium](#appium)
      1. [Woah...](#woah-woah-woah---that-was-a-lot)
      2. [Why Bother](#so-why-bother-if-its-so-hard-to-setup)
   2. [More...?](#more)
   3. [Example Mobile Projects](#example-mobile-projects-)

## Purpose

The purpose of this project is to show the types of projects and technologies I've worked on and written pertaining to software testing.  I want to do this so I can architect Software testing solutions.

All the work here I've either written from scratch or worked within heavily, and should understand to a high degree.

## Quality in the Context of Automated Software Testing

Quality in the context of Software testing is simply a standard. It's a standard we hold for our users, customers, stakeholders, ourselves, and the greater marketplace as a whole.

We can measure it in two ways: Quantitatively and Qualitatively.

- Quantitave quality refers to countable, measurable metrics: does a Web Application page load? Do I get a 200 response code from an API? etc. 

- Qualitative quality refers to standards that are subject to interpretation, and can even require intuition to understand.  As often the first "users" of an application, software testers need to anticipate scenarios confuse and give actual users wrong impressions.  For example, imagine if Google/Apple correct dark skin bias in smartphone technology in initial phases of development ahead of each other? Do they gain greater market shares earlier in the perennial phone where? Food for thought. 

Further discplines of Software testing such as Security Testing and Performance testing are simply combinations of the two:  

- Performance testing tools like Locust provide quantitative response times and failure rates we need to qualitatively determine whether they pass muster
- Security tools like OWASP Quantitativly can help determine if your website is secure or not versus a qualitative standard
- Accessibility standards like WCAG are Qualitative standards executed Quantitatively

The list goes on and on, but time is finite. 

Automated Software Testing helps us organizations and departments by cutting into the time it takes us to assess our applications on a variety of levels.

---

## Overall Methodology in Testing Automation Structure

For the most part, all Software Testing Projects consist of 3 to 4 parts(depending on how you look at it):

![img.png](img.png)

The 4 parts include Test Scripts, Step Definition, Application Control, and External Dependencies. Some tools combine all of these in one, but usually those have a cost associated with them.

Each layer should only interact within one degree of separation. For example your test scripts should not directly call your external dependencies.  This helps your project have clarity and flow not only when writing, but for maintenance in years/projects to come. 

Some tools combine Test Scripts and Step Definitions in one place.

### Test Scripts
Starting at the top, Test Scripts define what your tests will do and how they will run. For example, if you have chosen to use Cucumber to run your tests, at the highest level, your tests will look like this:

```agsl
@smoke_test @prod_deploy
Scenario: Load Website
    Given I go to the Google Home Page
    When I enter the search term "Google"
    Then the internet doesn't blow up
```
This is a test script, composed of steps. The code is pretty straight forward, to dig in on what is actually going on you would delve into the step definitions.

You can use tags like "@smoke_test" to control what tests run, and control in your pipeline what tests you want to run. 

Pretty much all testing tools have some way to control and manage suites of tests.

### Step Definitions

Tests are composed of Steps, and those Steps need to be defined in Step Definitions.(Not all test tools do this, but tests with this type of logic generally have more re-usability).

Steps definition be short and sweet if possible, and abstracted into other classes/methods with easy to read names. For example:

```agsl
When(/^I go to the Google Home Page$/) do |search_term|
  page = GoogleHomePage.new @browser
  page.go_to_home_page
end
```

Easy readable code that can be reused.

### Application Control

This layer is usually the real technical meat of a Software test project. It's where you combine application knowledge and external libraries to driver your application.

In WebApp projects, this layer is for your page objects and selenium.  In Mobile device projects, you got your Appium driver; in Api Test porjects, rest client code, etc.

I would include examples here, but the possibilities only extend as far as your technical abilities can take you.

The main factor that will drive development here are your dependencies and good coding practices/structure.  Be smart!

### External Dependencies

External dependency considerations for a test project are the same as all projects. Be smart and judicious about choices, and keep up with security concerns with new versions. 

It is especially important to keep an eye on open source libraries. Looking at your Ruby gem rest-client.


---


## Web Application Software Automation

Web Application Testing is the biggest use case of automated testing in the software industry.  As such, there's a lot of resources, tools, community, and knowledge widely available to automators.  I will discuss some of them here, but it's important to note what really separates good testers/automators in this space is fundamental understanding of core principles, rather than automating some point and click action.

### Tool choice for Webdriver Automation

In our diagram above, we mentioned how external dependencies fit in a Test Project architecture. Because WebApps(and "derivative" technology such as Hybrid mobile apps) are so popular, browser automation tool choice play a big part in determining the direction of your Automation project.

#### Free Tool: Selenium

Selenium, for example, is hands down the biggest player in this space. It is a **free** open source tool that has been around pretty much since the beginning browser automation.  However, Selenium is not actually built for test automators in mind.  Rather, you combine the use of this tool with other libraries and conventions to build a WebApp test suites.

This can allow you to be pretty flexible in your projects, but requires a greater degree of know how from maintainers of your test project, especially if you want to manage things like parallelzation and test reports efficiently.

#### Paid Tool: Cypress

On the other end of the spectrum, there are a lot of paid tools made specifically with testers in mind. In my opinion, [Cypress](https://www.cypress.io/) is the biggest up and comer taking over this space.

The best analogy I've heard comparing Selenium to Cypress is if Selenium is a tool that remote controls a browser, Cypress is a tool embedded within a browser. There are tons of out of the box features automator need to build big scalable projects that are too numerous to name here, and it looks really cool in action.

The reservations I have for really any tool like Cypress is you are really beholden to it.  You have to pay for licences. There's a flexibility you lack with it you might need on test suites that have complicated tests hitting APIs, Databases, etc.  The community is just not there yet. Cypress specifically does not support Firefox even.

This might not be too bad if you for example only want to automate components of Web Apps, you just need to make a wise choice for your shop.

### Example Web Automation Projects

I personally have been in the Web Browser automation game since I started my career. Here are some examples of Web Browser automation I have on my github page using Selenium([Watir](http://watir.com/)).  They are in Ruby, but I have worked professionally in Java as well:

- [Bare bones project that can serve as a starter for a Web App Automation project using Ruby, Watir, Cucumber](https://github.com/brandondjango/WebAppAutomation)

- [Name Game Testing project I did in 24 hours for a Job Interview Process](https://github.com/brandondjango/NameGameTesting)


---

## Mobile and Smart Device Automation

Mobile Device Automation can have a high bar to entry and maintain, but it can be a very useful tool in maintaining the quality of mobile applications and webapps.

The basic layout is the same as we mentioned before as far as overall structure. What seperates the mobile space from others is the pace at which it moves. Nearly every fall, major versions of Android and iOS(Apple mobile OS) are released. New devices and features are developed by companies ever competing to stay ahead of each other, and if you aren't keeping up with the landscape, you can catch yourself in a dependency/version specific nightmare.

Fortunately, living at that pace(at least at some point) is a good skill to have in your toolbelt :)

Another important skill to know about is Appium! 

### Appium

Appium is the biggest player in the mobile automation space. It is a library built on Selenium specifically for controlling/driving Mobile simulators and real devices.

Fortunately for us, it slots right into the external dependency/application control layer of our test project structure! For example, here is how you might open a Appium Driver for various devices, and control a browser on said device

```agsl
    def create_iphonex_safari_driver
        helper = DriverHelper.new
        helper.create_ios_simulator_safari(browserName: "Safari", platformVersion: "13.5", deviceName: "iPhone X")
    end    
```

From there, you will have access to an object that actually controls the device in realtime! You can use the driver to go to webpages, access elements on the page, etc.

Easy enough, right?

Well.... Lets look at that "create_ios_simulator_safari" method:

```agsl
    def create_ios_simulator_safari(browserName:, platformVersion:, deviceName:)
      #pull initial capabilities from template
      options = YAML.load(File.read(File.join(__dir__, "driver_templates/ios_simulator.yml")))

      #populate capabilities with arguments
      options["caps"]["browserName"] = browserName
      options["caps"]["platformVersion"] = platformVersion
      options["caps"]["deviceName"] = deviceName

      #create and start driver
      @driver = Appium::Driver.new(options, true)
      @driver.start_driver

      #return Appium driver
      return @driver
    end
```

And then that yaml template driver:

```agsl
#iOS simulator template

#no udid required for simulator
caps:
  platformName: 'iOS'
  #platformVersion: '11.0'  #Required
  #deviceName: 'iPhone 8'   #Required, grab from "xcrun simctl list"
  automationName: 'XCUITest'
  xcodeOrgID: '6N85WEFMZV'
  xcodeSigningId: 'iPhone Developer'
  newCommandTimeout: 1800
  clearSystemFiles: 'true'
  showXcodeLog: 'true'
  useCarthageSsl: 'true'
  updatedWDABundleId: '-N85WEFMZV.WebDriverAgentRunner'
  webkitResponseTimeout: 10000
  startIWDP: true

appium_lib:
  server_url: 'http://0.0.0.0:4723/wd/hub/'
```

And then there's the [setup to actually run Appium and get it connected to your devices.](https://github.com/brandondjango/MobileTestAutomation)

#### Woah Woah Woah - That was a lot

**Yup.** Keep in mind, we have not discussed factors like:
- Is my app native or hybrid?
- How many OS versions should I support?
- Should I maintain real devices, or run my automation on Virtual or Hosted devices?(BrowserStack for example will host virtual mobnile devices)

These are some of the first questions you need to answer *after* you make the decision to use Appium.

#### So why bother if it's so hard to setup?

**^Not the first time that question has been asked.**

In my opinion, the reason we want to use Appium is really the same as our other automation tools. Time savings, repeatability, removal of user error in test execution, repeatability, fast coverage. If anything, the savings in the fast paced world of mobile development increase in magnitude using automation.

It can just take a minute to get started.

### More?

Nope. There are too many considerations to further expand on this topic, but I'm always happy to have a conversation about it!

### Example Mobile Projects:

[Bare Bones Mobile Automation Project](https://github.com/brandondjango/MobileTestAutomation)





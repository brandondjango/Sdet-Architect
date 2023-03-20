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



## Web Application Software Automation

At all phases of my career I have worked
** Settings ***
Library           Collections
Library           Process
Library           RequestsLibrary
Library           SeleniumLibrary

*** Variables ***
${TESTS_DIR}   tests
${GITLAB_API_VERSION}   v4
${GITLAB_USERNAME}   fxs
${GITLAB_NAME}   jfxs
${GRID_URL}   http://selenium:4444/wd/hub
${BROWSER}   Chrome
${RF_SENSITIVE_VARIABLE}   ${EMPTY}

*** Test Cases ***
Test Robot Framework: [--version] option
    [Tags]    core    demo
    ${result} =    When Run Process    robot   --version
    Then Should Be Equal As Integers    ${result.rc}    251
    And Should Contain    ${result.stdout}    Robot Framework

Test mask sensitive variable:
    [Tags]    core    demo
    Log  Try to display my sensitive variable: ${RF_SENSITIVE_VARIABLE}
    ${result} =    When Run Process    echo   ${RF_SENSITIVE_VARIABLE}
    Then Should Be Equal As Integers    ${result.rc}    0

Test Requests library
    [Tags]    request    demo
    Given Create Session  gitlab  https://gitlab.com   disable_warnings=1
    ${resp}=  When Get Request  gitlab  /api/${GITLAB_API_VERSION}/users?username=${GITLAB_USERNAME}
    Then Should Be Equal As Strings  ${resp.status_code}  200
    ${user}=   And Get From List   ${resp.json()}   0
    And Dictionary Should Contain Item  ${user}  name   ${GITLAB_NAME}

Test Selenium library
    [Tags]    selenium    demo
    Given Open Browser	 https://www.google.com   ${BROWSER} 	remote_url=${GRID_URL}
    And Set Screenshot Directory	 EMBED
    And Wait Until Page Contains Element  name=q
    When Input text   name=q   robot framework
    And Wait Until Element Is Enabled  name=btnI
    And Scroll Element Into View   name=btnI
    And Click Element   name=btnI
    Then Wait Until Page Contains   Robot Framework
    And Capture Page Screenshot
    [Teardown]  Close All Browsers

*** Keywords ***

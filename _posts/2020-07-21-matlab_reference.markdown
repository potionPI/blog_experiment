---
layout: post
title:  "Matlab reference sheet"
author: Mint
date:   2020-07-21
category: Matlab
keywords: Quick look-up
abstract: "Check current directory, check files in current directory, for loop, while loop, functions, comments, ..."
---

* * * 

##### Check current directory:

    pwd

* * *

##### Check files in current directory:

    ls

* * *

##### For loop:

    for i = 1:10
        disp(i);
    end

for loop for array:

    myArray = [10, 13, -23];
    for i = 1:numel(myArray)
        disp(myArray(i));
    end

* * *

##### While loop:
    
    i = 1;
    while i <= 10
        disp(i);
        i = i + 1;
    end

* * *

##### Make a function:

    % Functions should be defined after all the code
    
    % Code here
    [a, b, c] = myFunction4();
    disp(a);
    disp(b);
    disp(c);
    
    % define functions below
    function x = myFunction1(parameter1, parameter2) % function with a return
        disp(parameter1);
        disp(parameter2);
        x = parameter1;
    end
    
    function myFunction2(parameter1, parameter2) % function without a return
        disp(parameter1);
        disp(parameter2);
    end
    
    function myFunction3() % function without parameters and no return
        disp("hi");
    end
    
    function [x, y, z] = myFunction4() % function with multiple returns
        x = 1; y = 2; z = 33;
    end
    
    %{
    Output would be:
    1
    2
    33
    %}

* * *

##### Commenting:

    % This is a one-line comment
    
    %{
        This is a block
        comment
    %}

* * *

##### Clear workspace

Matlab's clear workspace reference: [link](https://www.mathworks.com/help/matlab/ref/clear.html)

    clear %This clears EVERYTHING from the workspace area
    
    clear varA %This clears just the variable with name varA from the workspace area
    
    % To clear variables except a select few...
    varA = 1; varB = 1; varC = 1; varD = 1; varE = 1;
    clearvars -except varA varB varC; % Now varD and varE will disappear but the specified variables will not
    
* * *

##### Save and load workspace
Matlab's save and load workspace reference: [link](https://www.mathworks.com/help/matlab/ref/save.html)

save:

    save("myWorkspace"); % saves current workspace as myWorkspace.mat

load:

    load("myWorkspace"); % loads myWorkspace.mat into the workspace. Does NOT clear variables but will overwrite variables

* * *

##### Check if element is in vector

    myArray = [10, 20, 30];
    myElementToCheck = 10;
    myBoolean = sum(ismember(myArray, myElementToCheck));
    if myBoolean > 0
        disp(myElementToCheck + " is in array!");
    else
        disp(myElementToCheck + " is NOT in array!");
    end
    
* * *

##### Mac comment and uncomment shortcuts

To comment: COMMAND + /

To uncomment: COMMAND + T

* * *

##### Append more two arrays

Append more columns:

    A = [10, 20, 30];
    B = [22, 11, -10];
    C = [A, B]

Append more rows:

    A = [10, 20, 30];
    B = [22, 11, -10];
    C = [A; B]

* * *

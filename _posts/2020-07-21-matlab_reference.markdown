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

for loop for vector:

    myArray = [10, 13, -23];
    for i = 1:numel(myArray)
        disp(myArray(i));
    end
    
for loop for array matrix:

    myArray = [10 20 30 ; 40 50 60 ; 70 80 90];
    for i = 1:numel(myArray(:, 1))
        disp(myArray(i, 2));
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

##### dateshift

Shift some number of weeks or months

    z = datetime(2020, 1, 1); % January 1st 2020
    y = dateshift(z, 'end', 'week', 0); % y will now be the first (index 0) Sunday of January 2020 (January 4th 2020)
    y = dateshift(z, 'end', 'week', 1); % y will now be the second (index 1) Sunday of January 2020 (January 11th 2020)

* * *

##### swap columns

    % This swaps rows 2 and 3
    A = [1 2 3 ; 4 5 6; 7 8 9]
    A = A';
    temp = A(: , 2);
    A(: , 2) = A(: , 3);
    A(: , 3) = temp;
    
* * *

##### find element index in array

for array of strings

    ans3 = ["hello" , "hi" , "goodbye"];
    disp(find(strcmp(ans3,"hi")));

for array of numbers

    ans2 = [10, 2, 42];
    disp(find(ans2 == 42));

* * *

##### in a matrix or array, average all of the same of some column and make a new table

    table = [10 10 10 20 20 20 30 30 30; 1 1 1 2 0 4 -10 20 -1]';
    [~, ~, table2] = unique(table(:,1));
    table = [unique(table(:,1)) , accumarray(table2, table(:, 2),[], @mean)];

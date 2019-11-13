---
layout: post
title:      "Conditions, Using Arrays Vs Hard Coding"
date:       2019-11-13 00:58:16 +0000
permalink:  conditions_using_arrays_vs_hard_coding
---


Something as simple as changing a conditional based on a hard coded integer to an option that could change with your code could make or break your program. I learned this lesson whilst doing my project review for the first Learn.co module in the Software - Engineering program at Flatiron. It was pointed out to me that there was a fix to be made in my code, more specifically my conditional statement when choosing options based on a generated list through the program.

My conditional was initialing `if input.to_i > 0`, which means if the input put in by the user is greater than 0, run the code within the conditional. This is almost exactly what I wanted! However, I failed to remember that my list had a limit, and what would happen if the user's input is greater than the limit of my list, in this case 50. I had to change my conditional to accommodate my limits. 

I changed the conditional to `if input.to_i.between?(0, 50)` at first. This worked, however when I made the input that didn't exist within that range, let's say any symbol or letter, it chose the last option in the list and essentially broke my code, placing me in a location within my conditional that I could not locate. I could type other numbers and letters to see other options, however my 'exit' and 'list' options were not working as inputs. Thus brought me to the realization that I had to use a better solution. Enter the array.

For my project, the array that encapsulates my data was called "@horse". Taking this array, I could then make my conditional be: if input equals any number greater than 0 and less than 1 more than the total number of indexes in my array. This works wonders for many reasons. To start off, it allowed me to have a condition for my numbers that could possibly be entered, for my listy option, and for my exit option, without breaking the code. Also, if my array changed the total number of indexes within, the conditional would change with it. I wouldn't have to go back into the code to change it if that changes. 

All in all, through trial and error, I learned that hard coding has its time and place. However, more often than not, a program that is built to change around changes mad ein other parts of the program is better.


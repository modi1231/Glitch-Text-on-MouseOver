# Glitch-Text-on-MouseOver
Using JavaScript this shows how to scramble an element's text for a short period of time.. like it was 'glitching'.  

It was a pretty straight forward application of some jquery to get the text, get a random number from 1 to max length of the text, replace it with a randomly picked character from an array, and use it all in a timed looped function.

For the snippet here:
https://www.dreamincode.net/forums/topic/414359-glitch-text-on-mouseover/


=================
dreamincode.net tutorial backup ahead of decommissioning


 Posted 07 January 2019 - 12:35 AM 



Someone asked a question about how a site may have done a 'glitch effect' on a button.. looking into it the 'glitch' is actually just scrambling the text for a few seconds on mouse over.  

Checking into this and it was a pretty straight forward application of some jquery to get the text, get a random number from 1 to max length of the text, replace it with a randomly picked character from an array, and use it all in a timed looped function.

[code]<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title></title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
</head>
<body>
    <h1>Mouse over JS "glitch" text effect</h1>
    <blockquote>
        <u>Basic Overview:</u>
        <ol>
            Make a 'glitch' effect where the text changes randomly and then goes back to the original when moused over. <br />
            <br />
            <u>Needed:</u>
            <li>Random number</li>
            <li>Ability to get object's text</li>
            <li>Ability to change object's text</li>
            <li>Do so in a loop, but visible</li>
            <li>Put back the original text after leaving or a a second.</li>
        </ol>
    </blockquote>
    <hr />
    <p><u>Example:</u></p>
    <button id="TestButton">Test 123</button>
    <p id="demo" style="background-color:aliceblue;">&nbsp;</p>

    <script>

        //from: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random
        function getRandomInt(max)
        {
            return Math.floor(Math.random() * Math.floor(max));
        }

        $(document).ready(function ()
        {
            //Need to keep the existing text so this can be utilitzed on any 
            var existingValue = "";

            //Check to prevent the function to be called multiple times while still running.
            var isRunning = false;

            $("#TestButton").mouseover(function ()
            {
                // if this is already running don't run it again.  This would produce messed up text.
                if (isRunning) return;

                //If not running then set the flag.
                isRunning = true;

                // just showing when mouse over happens.
                $("#TestButton").css("background-color", "yellow");

                //Array of random characters to show.
                var foo = ["a",
                    "0",
                    "c",
                    "%",
                    "e",
                    "f",
                    "*",
                    "h",
                    "&",
                    "j",
                    "k",
                    "#",
                    "$",
                    "^",
                    "!",
                    "@"];

                //1.  Get the existing value of the element.
                existingValue = document.getElementById("TestButton").innerHTML;

                //2.  Get the length so the max is known on which to replace.
                var existingLength = document.getElementById("TestButton").innerHTML.length;

                //Set our demo element to show this works even without buttons.
                document.getElementById("demo").innerHTML = document.getElementById("TestButton").innerHTML;

                //3.  Making a time delayed loop.
                var i = 0;
                function TimeDelayedFunction()
                {
                    //https://www.w3schools.com/jsref/met_win_settimeout.asp
                    setTimeout(function ()
                    {
                        // 3.1  Get the random index value for the length of the element's text.
                        var ranMyB = getRandomInt(existingLength - 1);

                        //3.2  Get the random character to replace it with.
                        var ranRanText = foo[getRandomInt(foo.length - 1)];

                        //3.3 get the current object's text.
                        var bar = document.getElementById("TestButton").innerText;

                        //3.4  Use substring to do the replace.
                        bar = bar.substr(0, ranMyB) + ranRanText + bar.substr(ranMyB + 1);

                        //3.5  Set the element's text.
                        document.getElementById("demo").innerText = bar;//ranRanText;
                        document.getElementById("TestButton").innerText = bar;//ranRanText;

                        //3.6  Increase the counter
                        i++;

                        //3.7  Check if the "loop function" needs to happen again.
                        if (i < existingLength)
                        {
                            TimeDelayedFunction();
                        } else
                        {
                            //3.8  When done set to the original text.
                            document.getElementById("demo").innerHTML = existingValue;
                            document.getElementById("TestButton").innerHTML = existingValue;

                            //notify the function is done.
                            isRunning = false;
                        }
                    }, 80);//speed frequency.
                }

                //4 call the function.
                TimeDelayedFunction();

            });

            //$("#TestButton").mouseout(function ()
            //{
            //    // if the user mouse leaves the object then reset it all.
            //    $("#TestButton").css("background-color", "lightgray");
            //    document.getElementById("TestButton").innerHTML = existingValue;
            //    //isRunning = false;
            //});
        });
    </script>

</body>


</html>[/code]


https://github.com/modi1231/Glitch-Text-on-MouseOver
  

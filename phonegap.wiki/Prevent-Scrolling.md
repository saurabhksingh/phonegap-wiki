## About

In some cases, you may want to prevent the scrolling of a page. One of the most common scenarios is to prevent scrolling while displaying a dialog box to the user.

## How it Works

You can prevent scrolling by cancelling the touchMove event:

    element.addEventListener('touchmove', function(e) {
        // Cancel the event
        e.preventDefault();
    }, false);

## Example

### Prevent Scrolling on Everything

    <!DOCTYPE html>
    <html>
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
            <meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width;" />
            <script type="text/javascript">
                window.addEventListener('load', function() {
                    document.body.addEventListener('touchmove', function(e) {
                        e.preventDefault();
                    }, false);
                }, false);
            </script>
            <title>Mobile Web App</title>
        </head>
        <body>
            <div id="app">
                <!-- Add your content here -->
            </div>
        </body>
    </html>

### Prevent Scrolling on a Specific Element


    <!DOCTYPE html>
    <html>
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
            <meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width;" />
            <script type="text/javascript">
                window.addEventListener('load', function() {
                    document.getElementById('app').addEventListener('touchmove', function(e) {
                        e.preventDefault();
                    }, false);
                }, false);
            </script>
            <title>Mobile Web App</title>
        </head>
        <body>
            <div id="app">
                <!-- Add your content here -->
            </div>
        </body>
    </html>
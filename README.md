# JavaScript Countdown

A self-contained browser page showing the current local time and a countdown to **one hour after the page loads**.

The HTML, styles and JavaScript all live in [index.html](index.html). There are no package dependencies or build commands.

## Run

Clone or download the repository and open **index.html** in a modern browser.

If you prefer to serve it locally:

~~~bash
python3 -m http.server 8000
~~~

Visit http://localhost:8000. Python is optional and is only used to serve the static file.

## Behavior

- **Current time** shows local device time in 24-hour HH:MM:SS format.
- **Countdown** shows remaining hours, minutes and seconds.
- Both displays schedule updates approximately once per second.
- When the target is reached, the countdown displays **Countdown finished!**
- Reloading the page creates a new target one hour from that reload.

There is no start button: the timer starts when the page's script executes.

## How the countdown works

The target is created by adding 3,600,000 milliseconds to the current timestamp. Each countdown update subtracts the current time from that fixed target.

Hours, minutes and seconds are calculated with division, remainder and rounding down. This avoids relying on a counter that simply decrements once per scheduled callback.

Two functions handle the displays:

| Function | Purpose |
| --- | --- |
| **updateTime()** | Format the current local time and schedule its next update |
| **updateCountdown()** | Calculate remaining time, render it and stop scheduling when complete |

## Customize

Change the 3,600,000-millisecond offset to use a different duration. For example, five minutes is 300,000 milliseconds. Keep the visible heading consistent with the chosen duration.

Change the inline style block to adjust spacing, colors and typography.

## Limitations

The timer has no pause/resume control, alarm, user-entered duration or saved state. Browser suspension can delay visible updates. Because remaining time is derived from timestamps, it catches up when callbacks resume; changing the device clock can also change the result.

## Manual checks

1. Open the page and verify that both displays update.
2. Temporarily shorten the target offset to check the finished message.
3. Reload and confirm that a new countdown starts.
4. Leave the tab in the background, then return and inspect the remaining time.

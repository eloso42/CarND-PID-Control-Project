# Reflection

## Implementaiton of PID

In PID::Init() I initialize the PID coefficients with the given parameters
and the errors with 0.

PID::UpdateError() updates the P, I and D errors according to the given CTE.

PID::GetControl() returns the current control.

## Implementation of main

I have two instances of PID, one for the steering and one for the throttle.
The control value of both PIDs are truncated into the interval [-1,1].

As destination speed I chose 30 mph which is slow enough for good control
and quick enough to make it not too boring ;-).

## Choosing of PID coefficients

I started by setting I and D to zero and P to a small positive value. Then I
increased P until it would steer enough even in the sharpest turn on the track.
Then I increased D until it damped the oscillation enough for a smooth drive
on the straight. Finally I added a small value of I so it would run smoothly
also in turns but small enough to not overshoot too much when a turn changes
to a straight and vice versa.

## Limitations

Since the simulator does not send any timing data I assume that the time
between to messages is constant, which unfortunately is not always the case.
So in these (on my local machine rare, but in the online simulator regular)
cases, the I and D terms are not calculated correctly and the
control jerks a little bit.

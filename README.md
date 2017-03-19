# BIRDSTAR
A pico-8 commentary on climate change for the Linux Game Jam '17.

---

This cart was mostly just the result of me learning how to mess around with `memcpy()` -- it turns out that you can do some pretty fun stuff this way. The reflection at the bottom of the screen is created by grabbing part of the screen from memory and overwriting later addresses, in reverse row order. The 'ripple' is done by literally writing to addresses which are further ahead or slightly behind of the normal translation.

I wrapped this up as a very simple game, because I couldn't find an actual working example of a technique like this around the pico 8 community (though I found a couple of .gifs of other peoples' projects, so I knew it could be done). In the end I got a code snippet from the lexaloffle forums that I hacked a bit to do my thing:

```
mirrorcpy(0,128-32*2+1.5*sin(tick/60),0,128-32+1.5*sin(tick/60),128,128-32+1.5*sin(tick/60))

[...]

function mirrorcpy(sx,sy,dx,dy,w,h)
    if (sx+w>128) w=128-sx
    if (dx+w>128) w=128-dx
    if (sy+h>128) h=128-sy
    if (dy+h>128) h=128-dy
    w = w/2
    sad = 0x6000+flr(sy)*64+sx/2
    dad = 0x6000+127*64+dx/2 -- reflect
    for y=1,h do
        memcpy(dad,sad,w)
        sad+=64
        dad-=64-sin((y)/8)*cos(tick/64)
    end
end

```

I hope someone else finds this working example helpful!

This snippet was submitted to the Linux Game Jam 2017, mostly because it was totally made within the scope of the jam and I wanted to post it somewhere. Pico 8 is cross-platform and playable in several different ways, so maybe it will inspire some linux users to check out the other projects people have been making with it.

:beers: !

---

Awesome | .GIFs | PICO-8 Cart
:-------------------------:|:-------------------------:|:-------------------------:
<img src="https://github.com/mattleblanc/BIRDSTAR/blob/master/BIRDSTAR_1.gif?raw=true"> | <img src="https://github.com/mattleblanc/BIRDSTAR/blob/master/BIRDSTAR_2.gif?raw=true"> | <img src="https://github.com/mattleblanc/BIRDSTAR/blob/master/birdstar.png?raw=true">

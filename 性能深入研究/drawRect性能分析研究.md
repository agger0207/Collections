So if you’re trying to deal with a complex hierarchy and are deciding whether it’s better to use –[CALayer setShouldRasterize:] or to draw a hierarchy’s contents via CG, the only way to know is to test and measure.

When you implement drawRect or draw with CoreGraphics, you’re using the CPU to draw, 

https://lobste.rs/s/ckm4uw/a_performance-minded_take_on_ios_design/comments/itdkfh
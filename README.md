# Rust TMP100 and TMP101 Temperature Sensor Driver

[![crates.io](https://img.shields.io/crates/v/tmp100-tmp101.svg)](https://crates.io/crates/tmp1x2)
[![Docs](https://docs.rs/tmp100-tmp101/badge.svg)](https://docs.rs/tmp1x2)
[![Build Status](https://travis-ci.org/twilco/tmp100-tmp101.svg?branch=master)](https://travis-ci.org/twilco/tmp100-tmp101)
[![Coverage Status](https://coveralls.io/repos/github/twilco/tmp100-tmp101/badge.svg?branch=master)](https://coveralls.io/github/twilco/tmp100-tmp101?branch=master)
![Maintenance Intention](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)

This is a platform agnostic Rust driver for the TMP100 and TMP101
moderate-accuracy (±1°C), low-power, digital temperature sensors, using the
[`embedded-hal`] traits.

Much of this repository is based on [eldruin's tmp-1x2 driver repo](https://github.com/eldruin/tmp1x2-rs) - thank you Diego for your excellent work!  That driver is for the TMP-102 and TMP-112 devices, which work a little differently and thus require slightly different drivers.  My goal is to maintain similar APIs in every way to the `tmp-1x2` project whenever possible.

TODO: Update this section when more is known...

This driver allows you to:
- Change into one-shot or continuous conversion mode.
- Read the temperature.
- Enable/disable the extended measurement mode.
- Trigger a one-shot measurement.
- Read whether the one-shot measurement result is ready.
- Set the conversion rate.
- Set the high/low temperature threshold.
- Set the fault queue.
- Set the alert polarity.
- Set the thermostat mode.
- Read whether a comparator mode alert is active.

TODO: Link to blog post after it's written
[Introductory blog post](https://blog.eldruin.com/tmp1x2-temperature-sensor-driver-in-rust/)

## The devices

This driver is compatible with both the TMP100 and the TMP101 devices.

These temperature sensors are highly linear and do not require complex
calculations or lookup tables to derive the temperature. The on-chip
12-bit ADC offers resolutions down to 0.0625°C.

The TMP100 and TMP101 devices are digital temperature sensors ideal for 
negative temperature coefficient (NTC) and positive temperature coefficient 
(PTC) thermistor replacement. The devices offer a typical accuracy of ±1°C 
without requiring calibration or external component signal conditioning.

The TMP100 and TMP101 devices feature SMBus, Two-Wire, and I2C interface 
compatibility. The TMP100 device allows up to eight devices on one bus. The 
TMP101 device offers an SMBus Alert function with up to three devices per bus.

Datasheet: [http://www.ti.com/lit/ds/symlink/tmp100.pdf](http://www.ti.com/lit/ds/symlink/tmp100.pdf)

### Usage

TODO: Update this after the crate is actually written

Please find additional examples using hardware in this repository: [driver-examples]

```rust
extern crate linux_embedded_hal as hal;
extern crate tmp1x2;

use tmp1x2::{Tmp1x2, SlaveAddr};

fn main() {
    let dev = hal::I2cdev::new("/dev/i2c-1").unwrap();
    let address = SlaveAddr::default();
    let mut sensor = Tmp1x2::new(dev, address);
    let temperature = sensor.read_temperature().unwrap();
    println!("Temperature: {:.1}ºC", temperature);
}
```

## Support

For questions, issues, feature requests, and other changes, please file an
[issue in the github project](https://github.com/twilco/tmp100-tmp101).

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
   http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or
   http://opensource.org/licenses/MIT) at your option.

### Contributing

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.

[driver-examples]: https://github.com/eldruin/driver-examples
[`embedded-hal`]: https://github.com/rust-embedded/embedded-hal

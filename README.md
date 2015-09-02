# myojs-busyarm
A plugin for [Myo.js](https://github.com/thalmiclabs/myo.js) that detects when your arm is busy.

**[See it in action here](http://thalmiclabs.github.io/myojs-busyarm/demo/)** <small>(requires a myo!)</small>

`busyarm.myo.js` will emit a `arm_busy` event when the arm becomes busy and a `arm_rest` event when the arm is at rest. The variable `myo.isArmBusy` is a boolean that tracks what state the arm is in.

The library uses a [Exponential moving average](https://en.wikipedia.org/wiki/Moving_average#Exponential_moving_average) to smooth the gyroscope data. If the EMA goes above a certain threshold, the arm is considered busy.

```
Myo.on('arm_busy', function(){
	console.log('You are quite the hand talker');
});
Myo.on('fist', function(){
	if(!this.isArmBusy){
		this.trigger('calm_fist');
	}
})
```

Check out the [demo](/demo/index.html) for an example of how to use it.

#### configuration

```
Myo.plugins.busyarm = {
	threshold : 80,     //The threshold the EMA has to pass to be considered busy
	ema_alpha : 0.05,   //The coefficient for smoothing the EMA of the gyro data
};
```

You can use the demo to get an idea of a good threshold for you while doing different actions.
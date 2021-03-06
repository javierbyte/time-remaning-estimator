# Time Remaining Estimator.

Estimate the time remaining for any process with known progress (Exponentially Weighted Moving Average implementation).

# Usage

### Automatic Timestamp.
```js
const estimator = new TimeRemainingEstimator.auto({
  maxValue: 100
})

onProgress(function(newProgressValue) {
  /* once you register progress, you can add it to the estimate
   * to improve estimation
   */
  estimator.add({
    value: newProgressValue
  })

  estimator.calculate()
  // {finalDate: <dateObject>, remainingTime: <valueInMiliseconds>}
})
```

### Absolute Timestamp.
```js
const estimator = new TimeRemainingEstimator.absolute({
  maxValue: 100,
  startTime: processStartDate
})

onProgress(function(newProgressValue) {
  /* here you can add points at any time in any order
   * new points with the same time will override previous ones
   */
  estimator.add({
    value: newProgressValue,
    time: new Date()
  })

  estimator.calculate({
    time: new Date()
  })
  // {finalDate: <dateObject>, remainingTime: <valueInMiliseconds>}
})
```

### Functional Usage.
```
TimeRemainingEstimator.functional({
  maxValue: 100,
  startTime: <dateObject>,
  currentTime: <dateObject>,
  steps: [{
    time: <dateObject>,
    value: 1
  }, {
    time: <dateObject>,
    value: 3
  }, {
    time: <dateObject>,
    value: 23
  }, {
    time: <dateObject>,
    value: 55
  }]
})
// returns {finalDate: <dateObject>, remainingTime: <valueInMiliseconds>}
```

## How it works.
Implementation of https://en.wikipedia.org/wiki/Moving_average#Exponential_moving_average

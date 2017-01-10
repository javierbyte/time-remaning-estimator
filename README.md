# Time Remaining Estimator.

Estimate the time remaining for any process with known progress (Exponentially Weighted Moving Average implementation).

# Usage

```js
// with infered timestamp
const estimator = new TimeRemainingEstimator({
  total: 100,
})

onProgress(function(newProgressValue) {
  estimator.add({
    progress: newProgressValue
  })

  estimator.calculate()
  // {finalDate: <dateObject>, remainingTime: <valueInMiliseconds>}
})

// with absolute timestamp
const estimator = new TimeRemainingEstimator({
  total: 100,
  time: processStartDate
})

onProgress(function(newProgressValue) {
  estimator.add({
    progress: newProgressValue,
    time: new Date()
  })

  estimator.calculate()
  // {finalDate: <dateObject>, remainingTime: <valueInMiliseconds>}
})
```

## How it works.
Implementation of https://en.wikipedia.org/wiki/EWMA_chart

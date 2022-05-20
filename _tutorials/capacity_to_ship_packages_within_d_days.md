---
layout: post
title:  "Capacity to Ship Packages Within D Days"
categories: website
---

A conveyor belt has packages that must be shipped from one port to another within `days` days.

The `ith` package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `days` days.

### Initial Brainstorm

Given the data of `weights`, we should be able to determine whether some truck `capacity` will be sufficient to ship all the packages in `days` days.

Thinking about the simplest possible cases, we could either ship a package every single day, or we could ship all packages in one day.

This is because on the lower bound of truck capacity, the best case scenario would be that for each package from the conveyer belt, they all have identical weights, namely `max(weights)`, and will ship in `d = len(weights)-1`  days.

On the upper bound of truck capacity, the best case scenario would be that we have one truck with capacity `sum(weights)` such that all packages can be delivered in one day.

In reality, our cases will never perfectly fall into these situations, but somewhere in between!

There is some optimal value of the weight capacity such that it minimizes the days required to deliver, where the search space for our problem spans between `max(weights)` and `sum(weights)`. In other words, there is a value between the two such that every weight before it is unable to ship in the desired number of days, and every value after (including itself) will be able to ship in the desired number of days.

So now we have to determine our search space, how do we determine whether a given capacity will yield a successful delivery?

### Determining Whether We can Ship

So, we want to find out, given some maximum capacity of a truck, the weights of our packages, and the desired number of days, if we can ship all of the packages.

Given some capacity, notice that every instance that we have exhausted such a capacity, we would need another day to ship our packages. 

So, what we could do is iterate through our `weights`, subtracting `weights[i]` at each iteration from our current capacity, which essentially acts as loading these weights onto our ship until the maximal weight is exceeded. Once we have subtracted a `weights[i]` such that the evaluation is `≤ 0`, we require another day to ship.

If we do require another day to ship, we will reset our capacity back to the ships initial capacity, increase the required amount of days to ship by `1`, and continue this process until we have loaded all of our packages.

This is demonstrated in the below:

```python
def days_req(max_weight, weights, d):
		curr_days = 1
		capacity = max_weights
		n = len(weights)
		i = 0
		while i < n:
				if weights[i] <= capacity: 
						# If weights[i] <= capacity, there is room on the truck, thus 
						# remove weights[i] from capacity, and move on to the next package
						capacity -= weights[i]
						i += 1
				else:
					curr_days += 1 # There is no room on the truck, thus we need another day
					capacity = max_weights # and reset our capacity

		return curr_days <= d # required days <= desired days, return true.
```

And now that we have finished our logic for our binary decision, we now perform our binary search!

### Binary Search

So, given our `days_req(max_weight, weights, d)`, we can use its logic to determine how to cut down our search space as usual in binary search problems:

```python
def shipWithinDays(self, weights, days):
		min_weight, max_weight = max(weights), sum(weights)
		res = -1
		while min_weight <= max_weight:
				mid = (min_weight + max_weight) // 2
				if days_req(mid, weights, d):
						res = mid
						right = mid - 1
				else:
						left = mid + 1
		return res
```

## 爬楼梯
## 斐波那契
## 打劫房屋
#### 1.打劫房屋1  
描述
假设你是一个专业的窃贼，准备沿着一条街打劫房屋。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且 当相邻的两个房子同一天被打劫时，该系统会自动报警。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，在不触动报警装置的情况下, 你最多可以得到多少钱 。

[公式]dp[n] = max(dp[n-1], dp[n-2]+A[n])  
[code]:  
``` go
/**
 * @param A: An array of non-negative integers
 * @return: The maximum amount of money you can rob tonight
 */
import("math")
func houseRobber (A []int) int64 {
    if len(A) == 0 {
		return 0
	}
	if len(A) == 1{
		return int64(A[0])
	}
	if len(A) == 2{
		total := math.Max(float64(A[0]), float64(A[1]))
		return int64(total)
	}

	dp := make(map[int]int64)
	dp[0] = int64(A[0])
	dp[1] = int64(math.Max(float64(A[0]), float64(A[1])))
	for i := 2; i < len(A); i++{
		dp[i] = int64(math.Max(float64(dp[i-1]), float64(dp[i-2]+int64(A[i]))))
	}
	return dp[len(A)-1]
}
```  
#### 2.打劫房屋2
描述
在上次打劫完一条街道之后，窃贼又发现了一个新的可以打劫的地方，但这次所有的房子围成了一个圈，这就意味着第一间房子和最后一间房子是挨着的。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且 当相邻的两个房子同一天被打劫时，该系统会自动报警。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，在不触动报警装置的情况下, 你最多可以得到多少钱 。  
[思路]将圆化为直线  
[公式]   
[code]  

``` go
import("math")
func houseRobber2 (nums []int) int {
    // write your code here
	if len(nums) == 0 {
		return 0
	}
	if len(nums) == 1 {
		return nums[0]
	}
	if len(nums) == 2{
		return int(math.Max(float64(nums[0]), float64(nums[1])))
	}
	dp := make(map[int]map[int]int)
	dp[0] = make(map[int]int)
	for i := 0; i < len(nums)-1; i++{
		if i == 0 {
			dp[0][0] = nums[0]
		} else if i == 1{
			dp[0][1] = int(math.Max(float64(nums[0]), float64(nums[1])))
		} else {
			dp[0][i] = int(math.Max(float64(dp[0][i-1]), float64(dp[0][i-2]+nums[i])))
		}
	}
	dp[1] = make(map[int]int)
	for i := 1; i < len(nums);  i++ {
		if i == 1{
			dp[1][1] = nums[1]
		} else if i == 2{
			dp[1][2] = int(math.Max(float64(nums[1]), float64(nums[2])))
		} else {
			dp[1][i] = int(math.Max(float64(dp[1][i-1]), float64(dp[1][i-2]+nums[i])))
		}
	}
	return int(math.Max(float64(dp[0][len(nums)-2]), float64(dp[1][len(nums)-1])))
}
``` 

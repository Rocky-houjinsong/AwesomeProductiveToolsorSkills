[toc]

## Beginner Series #2 Clock

**Instructions**

Clock shows `h` hours, `m` minutes and `s` seconds after midnight.

Your task is to write a function which returns the time since midnight in milliseconds.

**Example:**

```
h = 0
m = 1
s = 1

result = 61000
```

Input constraints:

- `0 <= h <= 23`

- `0 <= m <= 59`
- `0 <= s <= 59`



**Solutions**

```powershell
function Past( 
	[ValidateRange(0,23)][int] $h, 
    [ValidateRange(0,59)][int] $m, 
    [ValidateRange(0,59)][int] $s) {
  # your code here
  $time = Get-Date -Hour $h -Minute $m -Second $s -UFormat %T
  ([TimeSpan]$time).TotalMilliseconds
}
```

```powershell
function Past([int] $h, [int] $m, [int] $s) {
  ([datetime]"${h}:${m}:${s}"-[datetime]"0:0:0").TotalMilliseconds
}
```

```powershell
function Past(
    [ValidateRange(0,23)][Int]$h,
    [ValidateRange(0,59)][Int]$m,
    [ValidateRange(0,59)][Int]$s
  ) {
  return [Timespan]::New($h, $m, $s).TotalMilliseconds
}
```



#### Grasshopper - Terminal game move function

**Instructions**

## Terminal game move function

In this game, the hero moves from left to right. The player rolls the dice and moves the number of spaces indicated by the dice **two times**.

Create a function for the terminal game that takes the current position of the hero and the roll (1-6) and return the new position.

### Example:

```python
move(3, 6) should equal 15
```


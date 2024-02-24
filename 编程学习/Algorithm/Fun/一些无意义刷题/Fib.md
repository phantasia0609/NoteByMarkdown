``` js
// 斐波那契数列递归
const fib = (n) => {
    if (n === 0 || n === 1) {
        return n;
    }
    return fib(n - 1) + fib(n - 2);
}

// 斐波那契数列递归优化
const fib2 = (n, memo = {}) => {
    if (n === 0 || n === 1) {
        return n;
    }
    if (memo[n] === undefined) {
        memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    }
    return memo[n];
}

// 斐波那契数列动态规划
const fib3 = (n) => {
    const dp = [0, 1];
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

// 斐波那契数列动态规划优化
const fib4 = (n) => {
    let prev = 0, curr = 1;
    for (let i = 2; i <= n; i++) {
        let sum = prev + curr;
        prev = curr;
        curr = sum;
    }
    return curr;
}

// 斐波那契数列动态规划优化
const fib5 = (n) => {
    let prev = 0, curr = 1;
    for (let i = 2; i <= n; i++) {
        [prev, curr] = [curr, prev + curr];
    }
    return curr;
}


```
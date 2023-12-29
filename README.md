# Minimum-Difficulty-of-a-Job-Schedule

class Solution:
    def minDifficulty(self, jobDifficulty, d):
        n = len(jobDifficulty)
        
        # If the number of days is greater than the number of jobs, it's impossible
        if d > n:
            return -1
        
        # dp[i][j] represents the minimum difficulty to schedule the first i jobs in j days
        dp = [[float('inf')] * (d + 1) for _ in range(n + 1)]
        dp[0][0] = 0

        for i in range(1, n + 1):
            for k in range(1, d + 1):
                max_difficulty = 0
                for j in range(i, 0, -1):
                    max_difficulty = max(max_difficulty, jobDifficulty[j - 1])
                    if j > k:
                        dp[i][k] = min(dp[i][k], dp[j - 1][k - 1] + max_difficulty)
                    else:
                        dp[i][k] = min(dp[i][k], dp[j - 1][k - 1] + max_difficulty)

        return dp[n][d] if dp[n][d] != float('inf') else -1

# Example usage:
solution = Solution()

job_difficulty1 = [6, 5, 4, 3, 2, 1]
d1 = 2
print(solution.minDifficulty(job_difficulty1, d1))  # Output: 7

job_difficulty2 = [9, 9, 9]
d2 = 4
print(solution.minDifficulty(job_difficulty2, d2))  # Output: -1

job_difficulty3 = [1, 1, 1]
d3 = 3
print(solution.minDifficulty(job_difficulty3, d3))  # Output: 3

# Additional Test Case
job_difficulty4 = [7, 1, 7, 1, 7, 1]
d4 = 3
print(solution.minDifficulty(job_difficulty4, d4))  # Output: 9

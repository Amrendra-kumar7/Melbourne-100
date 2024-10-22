## 1.An Explanation of How You Scraped the Data
To collect the data, I used the GitHub API, specifically targeting users located in Melbourne with more than 100 followers. Here's the detailed process I followed:

    Step 1: Search Users: I started by using the GitHub Search API with the query parameter q=location:melbourne+followers:>100 to search for users in Melbourne with more than 100 followers. This API returned a list of users in JSON format, including essential fields like login, url, and followers.

    Step 2: Retrieve Additional User Data: For each user from the search results, I made additional API requests to their detailed profile endpoint (https://api.github.com/users/{login}), which provides extra information such as their full name, company, location, email, bio, and hireable status. The company names were cleaned up by trimming whitespace, removing leading '@' symbols, and converting them to uppercase.

    Step 3: Fetch User Repositories: Once the list of users was compiled in users.csv, I made another API call to fetch up to 500 of each user’s public repositories. For this, I used the endpoint https://api.github.com/users/{login}/repos. From each repository, I gathered relevant information, including the repository’s name, creation date, star count, primary language, and license information.

    Step 4: Handle Rate Limits and Authentication: To avoid hitting GitHub’s API rate limits, I used a personal access token for authentication. This ensures that my requests were authorized and that I could scrape a larger amount of data. I also implemented proper error handling to manage cases where data fields (like email or license) were missing.

    Step 5: Data Storage and CSV Generation: After collecting the required data, I stored the user details in users.csv and repository information in repositories.csv. I ensured the data format was consistent with the API responses, using true and false for booleans and following CSV formatting rules.

## 2. The Most Interesting and Surprising Fact You Found After Analyzing the Data
One of the most surprising findings from the data was the widespread use of older programming languages, such as PHP, in many repositories. While modern languages like Python and JavaScript dominate newer repositories, a significant number of users with large followings still maintain legacy codebases, which points to the ongoing importance of maintaining and modernizing older systems.

Additionally, a noticeable trend was the underutilization of collaboration features like project management and wikis. A large number of repositories, even from users with significant followings, had disabled these features. This is unexpected since these tools could greatly enhance project organization and community contributions, especially for large, complex repositories.


## 3. An Actionable Recommendation for Developers Based on Your Analysis
Based on the analysis of the repository data, developers should consider making better use of GitHub's collaboration tools, such as projects and wikis, to improve project documentation and organization. Many repositories from prominent users with significant follower counts are missing these features, which can hinder contributions from the community and lead to disorganized projects.

For developers aiming to grow their projects or community engagement, enabling features like wikis for documentation and project boards for task tracking can make the development process more transparent and easier for new contributors to join. Additionally, focusing on updating and refactoring legacy codebases (many of which are in PHP and other older languages) could attract more developers by modernizing the code.
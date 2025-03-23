## Lets try to understand how is my HTML coverting the URL to open a Issue and how are the fields getting mapped : 

## Step 1: HTML Form Inputs
You have an HTML form with fields where users enter information:

- Book Title (id="title")
- Source (id="source")
- Reason (id="reason")

When the user clicks Submit, the form triggers this JavaScript: 

```javascript
document.getElementById('suggestion-form').addEventListener('submit', function(e) {
  e.preventDefault();
  
  const title = encodeURIComponent(document.getElementById('title').value);
  const source = encodeURIComponent(document.getElementById('source').value);
  const reason = encodeURIComponent(document.getElementById('reason').value);
  
  const githubUsername = 'your-username';
  const repoName = 'your-repo';

  const issueURL = `https://github.com/${githubUsername}/${repoName}/issues/new?title=📖%20Book%20Suggestion:%20${title}&body=**📚%20Title:**%20${title}%0A**🕵️‍♂️%20Source:**%20${source}%0A**💡%20Why%20I%20Love%20It:**%20${reason}`;

  window.location.href = issueURL;
});

```

👉 Explanation:

- encodeURIComponent() ensures special characters like spaces or emojis are converted to a URL-safe format.

- The issueURL is dynamically created using this data.

- Then, window.location.href = issueURL opens GitHub in a new tab, ready to create an issue.

##  Step 2: Understanding the URL Structure

- The URL is constructed like this:
```javascript

// Suppose a user submits:

// Title: "The Alchemist"
// Source: "Wattpad"
// Reason: "It made me believe in my dreams."

url = https://github.com/your-username/your-repo/issues/new
?title=📖%20Book%20Suggestion:%20The%20Alchemist
&body=**📚%20Title:**%20The%20Alchemist%0A
**🕵️‍♂️%20Source:**%20Wattpad%0A
**💡%20Why%20I%20Love%20It:**%20It%20made%20me%20believe%20in%20my%20dreams.

// %20 → Space
// %0A → New Line
// 📖 → Unicode Emoji

```

## Step 3: How GitHub Forms the Issue

- GitHub uses the URL to automatically generate a new issue with: 
- GitHub reads the URL query parameters (title= and body=).
- It converts markdown from the URL (**Bold Text**, emojis, line breaks) to proper formatting inside the issue.

```yaml
- Title: 📖 Book Suggestion: The Alchemist
- Body : 
    📚 Title: The Alchemist
    🕵️‍♂️ Source: Wattpad
    💡 Why I Love It: It made me believe in my dreams.

```

## so the url formed from html helps to make the perfect github issue

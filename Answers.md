# Butter

## Question 1

```Javascript
function retrieveFeelingQuote(category) {
  DOMSelectors.mainOutput.innerHTML = ""; //Gets rid of previous current quote
  $.ajax({
    method: "GET",
    url: "https://api.api-ninjas.com/v1/quotes?category=" + category,
    headers: { "X-Api-Key": "e83S07p6GaMOgL3Tbp4W7g==SzjBmXqoFLEGxuow" },
    contentType: "application/json",
    success: function (result) {
      console.log("Retrieved Quote:", result); //Check: Quote Retrieval
      const quoteObject = {
        author: result[0].author,
        quote: result[0].quote,
        category: category,
      };
      quoteHistory.push(quoteObject); //Quote added to long term storage (History)
      console.log("History of Quotes:", quoteHistory); //Check to see if in long term
      quoteCurrent.length = 0; //Empty quoteCurrent
      quoteCurrent.push(quoteObject); //Quote added to short term storage (Current Quote)
      // Display the quote on the page
      console.log("Current Quote:", quoteCurrent); //Check to see if current quote works
      for (let i = 0; i < quoteCurrent.length; i++) {
        const quote = quoteCurrent[i];
        createQuoteCard(quote);
      }
    },
    error: function ajaxError(jqXHR) {
      console.error("Error: ", jqXHR.responseText);
    },
  });
}
```

Input = Categories of quotes
Function = Grabs the API and converts it into a Json file. If it successfully fetches the item, it creates an object that has the item's author, quote, and category. It puts this quote into a history and then pushes the quote into a temporary

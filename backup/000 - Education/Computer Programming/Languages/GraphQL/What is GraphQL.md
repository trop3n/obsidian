---
up: "[[GraphQL]]"
tags:
  - "#education/computerprogramming/languages/graphql/whatisgraphql"
prev: "[[How To GraphQL]]"
source: https://hygraph.com/learn/graphql
---

# Key Takeaways


- GraphQL is a modern query language and a runtime for APIs, widely seen as as successor to REST APIs.
- GraphQL is built around the concept of "getting exactly what you asked for" without any data under or overfetching.
- GraphQL makes it easier to aggregate data from multiple sources. It uses a type system rather than multiple endpoints to describe data.
- The [GraphQL Landscape](https://landscape.graphql.org/) shows an aggregated GraphQL adoption table covering over 116k stars, a market cap of $4.7 Trillion, and a funding of over $9 billion.
- The team at [Honeypot](https://honeypot.io/) filmed [a documentary](https://www.youtube.com/watch?v=783ccP__No8) on the history and emergence of GraphQL.

By now, GraphQL is no longer the "new kid on the block". You've probably heard of it and its [comparison with RESTFUL APIs](https://hygraph.com/blog/graphql-vs-rest-apis). However, if you are new to using this query language and want to learn how to use it, Hygraph’s GraphQL academy is your place to be.

Being in the [GraphQL field for almost as long as it exists](https://hygraph.com/blog/graphcms-is-now-hygraph), we are profoundly passionate about this topic and want to share our knowledge with you. You'll find everything you need, from the most basic concepts like how GraphQL works to usage topics like GraphQL schema, mutation, subscription, and many more.
# What is GraphQL?

Simply put, GraphQL is a [query language for APIs](https://graphql.org/) and a runtime for fulfilling those queries with existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they needs and nothing more, makes it easier to evolve APIs over time, and enables [powerful developer tools](https://hygraph.com/blog/graphql-tools).

GraphQL supports reading, writing ([mutating](https://hygraph.com/learn/graphql/mutations)), and [subscribing](https://hygraph.com/learn/graphql/subscriptions) to changes to data (real-time updates -- most commonly implemented with WebhHooks). GraphQL servers are available for multiple languages, including Haskell, JavaScript, Perl, Python, Ruby, Java, C++, C#, Scala, Go, Erlang, PHP and R.

> [!NOTE] Editor's Note
> These are developers' favorite languages for working with GraphQL, according to our [2024 GraphQL survey](https://hygraph.com/graphql-survey-2024#how-developers-build-graphql-apis).
> 
> 1. TypeScript/JavaScript
> 2. Go
> 3. Java/Kotlin
> 4. C#/.Net
> 5. Rust
## How Does GraphQL Work?

The attraction of GraphQL is primarily based on the concept of asking for what you need and receiving just that -- nothing more, nothing less. When sending queries to your API, GraphQL returns a very predictable result without any over- or under-fetching, ensuring that apps using GraphQL are fast, stable and scalable.

Using our website as an example, let's run a query asking for jus the titles of articles under the [Hygraph Academy](https://hygraph.com/learn) to visualize how this would look.

The query would look similar to this:

```json
{
  academyPosts {
    title
  }
}
```

From here, we can infer that we're just asking for the `title` of Academy posts and nothing else. Therefore, the results returned would be:

```json
{

  "data": {

    "academyPosts": [

      {
        "title": "Headless Mobile Content Management System (Mobile CMS)"
      },
      {
        "title": "What is Content as a Service (Caas)"
      },
      {
        "title": "Headless CMS and SEO Best Practices"
      },
      {
        "title": "What Is A Headless CMS?"
      },
      {
        "title": "Understanding Digital Experience Platforms (DXP) and Headless CMS"
      },
      {
        "title": "Understanding the Content Mesh and how a Headless CMS fits in."
      },
      {
        "title": "The Era of Application Content"
      },
      {
        "title": "Best Practices for Headless Content Modelling"
      },
      {
        "title": "Choosing the best Headless CMS"
      },
      {
        "title": "What is GraphQL?"
      },
      {
        "title": "Choosing a Headless CMS for Content Creators"
      },
      {
        "title": "Selecting a Headless CMS - a Checklist"
      },
      {
        "title": "What is a DXP (Digital Experience Platform)?"
      },
      {
        "title": "What is the JAMStack?"
      }
    ]
  }
}
```

It is easy to highlight how the payload would be minimal on such a simple request. However, GraphQL queries access not just the `fields` of a single resource but also follow references between them. While typical REST APIs require loading from multiple URLs, GraphQL APIs get all the data in a single request -- making apps quick even on slow mobile network connections.

To visualize this, let's try a more complex request: We want to see a list of blog posts on Hygraph, but rather than just the `post title`, we also want to get the `authors` these posts are related to, the `slugs` of the posts, and the `categoris` these blog posts fall under. 

The query we'll use for this is:

```json
{

  blogPosts{
    title
    authors {
      name
      twitterHandle
      title
    }
    slug
    categories {
      title
    }
  }
}
```

The results given back (shorted to just one) look like:

```json
{
  "data": {
    "blogPosts": [
      {
        "title": "Delivering a DIY Store powered by a Headless CMS for ECommerce",
        "authors": [
          {
            "name": "Jamie Barton",
            "twitterHandle": "notrab",
            "title": "Developer Advocate"
          },
          {
            "name": "Jonathan Steele",
            "twitterHandle": "ynnoj",
            "title": "Developer Advocate"
          }
        ],
        "slug": "delivering-a-diy-store-powered-by-a-headless-cms-for-ecommerce",
        "categories": [
          {
            "title": "Content Management"
          },
          {
            "title": "Headless CMS"
          },
          {
            "title": "Projects and Examples"
          }
        ]
      }
}
```

**GraphQL APIs are organized in terms of fields and types, not endpoints**, making them extremely easy to get up and running since you can access all your data from a single endpoint. GraphQL uses types to ensure apps only ask for what's possible and provide clear and helpful errors. Apps can use types to avoid writing manual parsing code.
## Why GraphQL?

As you learn [how GraphQL works with some examples](https://hygraph.com/learn/graphql#how), it should be apparent that it is fast, stable and scalable. In summation, these are the 3 key characteristics that make GraphQL a dream syntax to use:

1. Clients can specify exactly what data they need.
2. Aggregating data from multiple sources is easy with GraphQL
3. GraphQL uses a type system to describe data rather than endpoints

These characteristics make GraphQL data fetching utterly efficient, and offer benefits including easy readability, avoiding under and over-fetching, strong typing, and flexible schema evolution -- Discover [GraphQL's advantages in more detail here](https://hygraph.com/blog/graphql-advantages).
## The History of GraphQL

Similar to React, GraphQL was developed internally by Facebook in 2012 before being publicly released in 2015. Following GraphQL's transition to being made open source, the GraphQL project was moved from Facebook to the newly established [GraphQL Foundation](https://graphql.org/), hosted by the Linux Foundation, in 2018.

The origin of GraphQL comes from [Facebook's attempts to scale its mobile app](https://hygraph.com/blog/products-using-graphql#meta-from-mobile-applications-to-the-meta-app-rewrite) At the time, their app was an adaptation of their website, and their mobile strategy was to simply "adopt" HTML5 to mobile. Due to issues related to high network usage and less-than-ideal UX, the team decided to build iOS from scratch using native technologies. 

[Brenda Clark](https://levelup.gitconnected.com/@brenda.clark) put the history of GraphQL quite well on [LevelUp's post](https://levelup.gitconnected.com/what-is-graphql-87fc7687b042):

> [!NOTE]
> > The main problem with Facebook’s News Feed implementation on mobile. It wasn’t as simple as retrieving a story, who wrote it, what it says, the list of comments, and who’s liked the post. Each story was interconnected, nested, and recursive. The existing APIs weren’t designed to allow developers to expose a rich, news feed-like experience on mobile. They didn’t have a hierarchical nature, let developers select what they needed, or the capability to display a list of heterogeneous feed stories.
> 
> Brenda Clark

Long story short, the core team at Facebook decided they needed to build a new News Feed API, which is when GraphQL began to take shape. Over the next several months, the surface area of GraphQL expanded to cover most of the Facebook iOS app, and in 2015, the GraphQL spec was first published along with the reference implementation in JavaScript.

The team at [Honeypot](https://honeypot.io/) made a comprehensible [documentary on YouTube](https://www.youtube.com/watch?v=783ccP__No8) about the birth and adoption of GraphQL, providing a highly detailed insight into the technology's emergence.
## Adoption of GraphQL

Understandably, GraphQL's adoption skyrocketed since the industry's need for such a solution was quite prevalent. Within half a year, there were already implementations of GraphQL in different languages, like PHP, JavaScript, Python, Scala and Ruby.

Starting as a "hobbyist" spec, GraphQL rapidly gained enterprise validation and was adopted by companies like GitHub, Yelp, AirBnB, and many more. 

The [GraphQL Landscape](https://landscape.graphql.org/) shows an aggregated GraphQL adoption table covering over 222k stars, a market cap of $4.7 trillion, and over $9 billion funding.

Between all the GraphQL servers, clients, gateways, and apps, the GraphQL ecosystem has exploded in market adoption, claiming GraphQL's spot as a force to reckon with.


> [!NOTE] Editor's Note
>Here’s an article that describes [when and when not to use GraphQL](https://hygraph.com/blog/is-graphql-right-for-your-project) and whether it's the right choice for you if you're considering adopting it. In addition, we’ve also examined [companies that use GraphQL in production](https://hygraph.com/blog/products-using-graphql).

## GraphQL vs. REST

A REST API is an "[architectural concept](https://www.rubrik.com/blog/graphql-vs-rest-apis/)" for network-based software. GraphQL, on the other hand, is a query language and a set of tools that operate over a single endpoint. Over the last few years, REST has been used to create APIs, while GraphQL has been mainly used to optimize performance and stability. 

When using REST, you'll always be returned compete "datasets". If you wanted to request information from `x` objects, you'd need to perform `x` REST API requests. If you're requesting information on a product for an eCommerce website, your requests may be structured in this way:

- Request `productInfo` for product names, descriptions, etc. in one request
- Request `pricing` for prices pertaining to that product in another request
- Request `images` for products shots from another request
- ...and so on.

While you'll still get everything you asked for, it would be done in several requests, and each dataset might send you tons of other information you didn't want or need, such as reviews, variations, discounts, etc.  depending on how the content/data was structured at each endpoint. On one hand, this is extremely simple - you have one endpoint that does one task, so it's easy to understand and manipulate. In other words, if you have X endpoint, it provides X data.

Conversely, if you wanted to gather some information from a specific endpoint, [you couldn’t limit the fields that the REST API returns](https://www.rubrik.com/blog/graphql-vs-rest-apis/); you’ll always get a complete data set - or over fetching.

GraphQL uses its query language to tailor the request for exactly what you need, from multiple objects down to specific fields within each entity. GraphQL would take X endpoint and it can do a lot with that information, but you have to tell it what you want first.

Using the same example, the request would simply be to get `productName`, `productDescription`, `productImage`, and `productPrice` from the same endpoint, within one request, and no more. All other content within the database wouldn't be returned, so the issue of overfetching wouldn't be a concern. 

For an amusing ELI5 on the topic, [Ben Halpern](https://github.com/benhalpern), the founder of [dev.to](https://dev.to) explains the [conceptual differences between GraphQL and REST](https://dev.to/ben/comment/hdi). Worth a read.
## Frequently Asked Questions

### What is GraphQL?

GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data.

### Is GraphQL better than REST?

It depends on the use case. However, the most commonly stated benefit is that GraphQL solves both over-fetching and under-fetching issues by allowing the client to request only the data that is required. Since there is more efficiency associated with working with GraphQL, development is much faster with GraphQL than it would be with REST.

### Is GraphQL faster than REST?

GraphQL queries themselves are not faster than REST queries, but since you have full control over what you want to query and what the payload should be, GraphQL requests will always be smaller and more efficient. GraphQL also enables developers to retrieve multiple entities in one request, from one endpoint, further adding to each query's efficiency.

### Why is GraphQL so popular?

GraphQL is commonly associated with a better developer experience through team independence and making API versioning redundant. A strongly typed schema, declarative data fetching, and predictable code & payload are other reasons why GraphQL is favored.

### How can I learn GraphQL?

If you’re just getting started with GraphQL, [Hygraph's GraphQL Academy](https://hygraph.com/learn/graphql), [How to GraphQL](https://www.howtographql.com/), and [FreeCodeCamp](https://www.freecodecamp.org/news/a-beginners-guide-to-graphql-86f849ce1bec/) are great places to start.

### Why use a GraphQL CMS?

Hygraph is a 100% GraphQL Headless CMS. The advantage here is that you can build projects with minimum payload, client-driven data queries, generated documentation, powerful tooling, and extensive filtering for an utterly flexible interaction with your API. The [generated GraphQL API](https://hygraph.com/headless-cms) works for read and write operations and scales seamlessly.
# Schemas and Types

> Let's take a look into what GraphQL Schemas and Types are.



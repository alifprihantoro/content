> this not complete yet
example code :
```javascript
const getFeed = async () => {
  const MAX = 5;
  const BLOG_NAME = "pawartatech";
  const ORDER_BY = "updated"; // updated, starttime
  const START_INDEX = 1;
  const URL_FEED = `https://${BLOG_NAME}.blogspot.com/feeds/posts/summary?alt=json&max-results=${MAX}&start-index=${START_INDEX}&orderby=${ORDER_BY}`;
  const CONTENT = await fetch(URL_FEED).then((res) => res.json());

  const FEED = CONTENT.feed;
  const isNext = FEED.link.some(({ rel }) => {
    if (rel === "next") {
      return true;
    }
  });

  const LIST_CONTET = FEED.entry;
  return { isNext, LIST_CONTET };
};
getFeed();

const LIST_FEED = await getFeed();
const ListEl = LIST_FEED.LIST_CONTET.map(
  ({ published, updated, title, summary, link, author }) => {
    return `
--
published: ${published["$t"]}
updated: ${updated["$t"]}
title: ${title["$t"]}
summary: ${summary["$t"]}
link: ${link
      .map(({ rel, href }) => {
        if (rel === "alternate") {
          return href;
        }
      })
      .join("")}
author:
${author.map(({ name, gd$image }) => {
  return `
name = ${name["$t"]}
img = ${"https:" + gd$image.src || ""}
`;
})}
`;
  },
);
console.log(ListEl[0]);
if (LIST_FEED.isNext) {
  console.log("next");
}

```

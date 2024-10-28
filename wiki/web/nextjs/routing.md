# Nextjs routing

[◀ Back](../index.md)

## Resources

- [Mastering Nextjs Routing](https://medium.com/@farihatulmaria/mastering-next-js-routing-an-in-depth-guide-to-advanced-features-5aa10e15ec7f) - paid resource for typescript learning
- [nexjs.org/docs/../routing](https://nextjs.org/docs/app/building-your-application/routing) - Official documentation about nextjs routing


### Dynamic routing

Base routing build on the file structure

    pages/index.js → /
    pages/about.js → /about
    pages/contact.js → /contact


Nested routes are created by creating a folder with the same name as the file and adding an `index.js` file inside it.

    pages/blog/index.js → /blog
    pages/blog/post.js → /blog/post


For dynamic routing you can use the `[]` brackets in the file name.

    pages/post/[id].js → /post/:id
    pages/post/[id]/comment.js → /post/:id/comment


Catch-all routes are created by using `...` in the file name.

    pages/post/[...slug].js → /post/:slug
    pages/post/[...slug]/comment.js → /post/:slug/comment


Optional Catch-All Routes are created by using `[[...slug]]` in the file name.

    pages/blog/[[...slug]].js → Matches /blog, /blog/post1, /blog/category/post, etc.


    

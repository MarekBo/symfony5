# More Queries

Coming soon...

So now that our show page is working, let's bring the homepage to life. These are
still just too hard, coded questions this time. Instead of querying for one question
object, we want to query for all of the question objects in the database. So let's
spin over and go to our question controller and scroll up to the homepage. So we now
know how to query. We can get the entity manager, interface, entity manager
arguments, and then down here, the next thing we do is we get the repository with
repository = and steam manager, interface it, repository question one, colon class.
So, I mean, I have this repository object. That's really good at querying from the
question table. Finally, we can say questions,

Questions = repository, arrow, find all. So find all is going to return to us the
array of all the question objects in the database. Well, prove it by saying D D
questions, and then we move over and refresh. There we go. All the 11 question
objects I have in my database. All right, now we are dangerous because we can pass
these into our template. So I'll add a second argument to render, to pass a question.
Variable set to our array of question objects. All right. Let's pop open that
templates question homepage that age, HTML twig, and let's see on the homepage right
now. Don't show that on the homepage right now we have two hard coded questions. So
actually what I want to do here is loop right here. Say for question in questions,
and then in a second, we'll make all of this stuff dynamic, but let's trace this line
down here. Here's where it ends. And then I'll say and four, and we can delete the
second hard coded question.

Perfect. Now it's just like the show page. We have a question variable, and instead
of here we can make things dynamic. So let's see the first spot down here is with the
question title with the question name. So let's, I'll say curly curly question, that
name, and then the slug here also needs to be dynamic. So we'll say question that
slug, and then down below here, this text here is actually the question itself. So we
can say curly curly question, that question pipe, we'll parse that through markdown.
And then I'll ask about here. We needed somebody dynamic is once again, there's
another link at the bottom and we want to print a question that slug. And so you can
see really quickly doctrines, make it easy for us to query our objects. Twig makes it
easy to render them. And we have a dynamic home page with all of our questions.

So if you remember, you can kind of see this by clicking into it. Every question has
a random asked at date, so you can see different asks, asked dates. And in reality,
what we probably want is to have the newest ones on top of the page. So we really
want to do this same query. We want to reorder it. If I click on the web debug
toolbar right now, you can see the query. It looks like we expect, it's basically
selecting all of the columns from question, but there's no order by on it. Now, when
you're working with the built the methods on the repository class, they're not very
flexible. They can't do too many flexible things. For example, find all doesn't have
any parameters. There's no way for us to order that. But so eventually we're going to
need to write a custom query when we want to do more complex stuff, but actually we
can use the font.

These built in methods to reorder this we're going to do here is say, fi is used.
Find by now we'll find by does, is it takes an array of where clauses. So you can say
things like where slug equals, you know, foo or something like that. But in this
case, we don't really want to have anywhere clauses so we can leave that empty. But
the fine by a method does have a second argument, which is an order by. So here we
can pass it in array with asked, at, asked at set, uh, equal arrow, D E S C.

So now I'm going to go over and refresh and we didn't kind of click in here. We can
say yes, 10 days ago for the first one and for the second one, one month ago. So it
looks right and we can kind of confirm by looking at the query and the web. You have
to have our yes. Order by ASP, add this sending perfect, but we've pushed our built
in methods about as far as they can go next, we're going to further, we're gonna make
this Macquarie for this page more complex, so complex that we're going to need to
write a custom query to accomplish it.

Now when you call get repository, what that actually gives you back? Isn't a class
called entity repository. So all shifts. Okay. Inside entity, repository .php. I want
to actually see what that looks like and I'll make sure I include all non project
items here. There we go. So NC repository, which lives deep down inside of doctrine.
So this is actually the object that we get back and you can see it has methods on it,
like down here, find, find out, yeah, find a buy, find one, buy. So time you call,
get repository. You get back an instance of entity repository. And this is where all
those methods live. But check this out. Okay. I'm going to DD repository. When I move
over now and refresh, check this out, it is not actually an instance of entering
repository. It's an instance of app repository, question repository. That's a class
that lives in our project. Open it up and source repository, question repository or
adopt PHP. Now remember when we originally ran a make entity to generate our question
entity, it generated two classes. It generated our question class, but it also
generated question repository. And at that time I said, don't worry about this. We'll
talk about it later. Now, if you look closely questioned, repository extends this
service entity repository. And if you hold command or control and click into that,
that extends entity repository. The class we were just looking at.

So the point is this question, repository class extends entity repository, which is
why we have all, which is why we can use all the methods, like find all our find by
now, the reason that doctor knows to give us a question repository. When we ask for
the, when we call get repository and pass it. The question is at the top of the
question class, we have an ad or an entity, and it says repository class = question
repository, ::class. This was generated for us from make entity. So the whole point
is that whenever we call a get repository and pass it, the question class, it's going
to give us back an instance of question repository, and that has all the shortcut
methods in it. We need now reason. This is cool is that each time we need to write a
custom query, we can add a new method inside of the question repository for it.

So you can actually see one generated in here by default. I'm actually going to
comment out this find by example, field thing here. So if I have a fine by example
field method in here, I can actually call that on my repository because this is an
instance of question repository. So in our case, well, we, what I want to do next is
modify the query in here. Not just to order by asked at, but I also want to add where
asked to add is not, no, because I don't want to show a questions that don't have an
AskPat value, but doing an ease, not know is too complex for the fine buy. So we're
going to need to custom query. So in question repository, I'm going to rename this
method to find that all asked, ordered by newest. And we won't need this to take any
arguments. And then inside of my controller, I'll get rid of the D D we can say
questions = repository arrow. Find all asked, ordered by newest. Of course, that's
not going to work yet because this logic is all wrong. But next let's learn about
what this query builder thing is and learn how we can make a custom query that
returns the exact question objects that we need.

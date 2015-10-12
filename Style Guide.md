Style Guidelines
================

In order to keep the code consistent, please use the following conventions. From here on \`good' and \`bad' are used to attribute things that would make the coding style match, or not match. It is not a judgment call on your coding abilities, but more of a style and look call. Please try to follow these guidelines to ensure prettiness.

You may also wish to read the [.Net Framework Design Guidelines](http://msdn.microsoft.com/en-us/library/ms229042.aspx) as well, however the Mono guidelines below take precedent for Mono code if there is a conflict.

Indentation
-----------

Use tabs (and configure your IDE to show a size of 8 spaces for them) for writing your code (hopefully we can keep this consistent). If you are modifying someone else's code, try to keep the coding style similar.

Since we are using 8-space tabs, you might want to consider the Linus Torvalds trick to reduce code nesting. Many times in a loop, you will find yourself doing a test, and if the test is true, you will nest. Many times this can be changed. Example:

``` csharp
for (i = 0; i < 10; i++) {
    if (something (i)) {
        do_more ();
    }
}
```

This takes precious space, instead write it like this:

``` csharp
for (i = 0; i < 10; i++) {
    if (!something (i))
        continue;
    do_more ();
}
```

 Switch statements have the case at the same indentation as the switch:

``` csharp
switch (x) {
case 'a':
    ...
case 'b':
    ...
}
```

Performance and Readability
---------------------------

It is more important to be correct than to be fast.

It is more important to be maintainable than to be fast.

Fast code that is difficult to maintain is likely going to be looked down upon.

Where to put spaces
-------------------

Use a space before an opening parenthesis when calling functions, or indexing, like this:

``` csharp
method (a);
b [10];
```

Do not put a space after the opening parenthesis and the closing one, ie:

good:

``` csharp
method (a);
array [10];
```

bad:

``` csharp
method ( a );
array[ 10 ];
```

Do not put a space between the generic types, ie:

good:

``` csharp
var list = new List<int> ();
```

bad:

``` csharp
var list = new List <int> ();
```

Where to put braces
-------------------

Inside a code block, put the opening brace on the same line as the statement:

good:

``` csharp
if (a) {
    code ();
    code ();
}
```

bad:

``` csharp
if (a)
{
    code ();
    code ();
}
```

Avoid using unnecessary open/close braces, vertical space is usually limited:

good:

``` csharp
if (a)
    code ();
```

bad:

``` csharp
if (a) {
    code ();
}
```

Unless there are either multiple hierarchical conditions being used or that the condition cannot fit into a single line.

good:?

``` csharp
if (a) {
    if (b)
        code ();
}
```

bad:

``` csharp
if (a)
    if (b)
        code ();
```

When defining a method, use the C style for brace placement, that means, use a new line for the brace, like this:

good:

``` csharp
void Method ()
{
}
```

bad:

``` csharp
void Method () {
}
```

Properties and indexers are an exception, keep the brace on the same line as the property declaration.

Rationale: this makes it visually simple to distinguish them.

good:

``` csharp
int Property {
    get {
        return value;
    }
}
```

bad:

``` csharp
int Property
{
    get {
        return value;
    }
}
```

Notice how the accessor "get" also keeps its brace on the same line.

For very small properties, you can compress things:

ok:

``` csharp
int Property {
    get { return value; }
    set { x = value; }
}
```

 Empty methods: They should have the body of code using two lines, in consistency with the rest:

good:

``` csharp
void EmptyMethod ()
{
}
```

bad:

``` csharp
void EmptyMethod () {}
```

``` csharp
void EmptyMethod () {
}
```

``` csharp
void EmptyMethod ()
{}
```

If statements with else clauses are formatted like this:

good:

``` csharp
if (dingus) {
        ...
} else {
        ...
}
```

bad:

``` csharp
if (dingus)
{
        ...
}
else
{
        ...
}
```

bad:

``` csharp
if (dingus) {
        ...
}
else {
        ...
}
```

Classes and namespaces go like if statements, differently than methods:

good:

``` csharp
namespace N {
    class X {
        ...
    }
}
```

bad:

``` csharp
namespace N
{
    class X
    {
        ...
    }
}
```

So, to summarize:

| Statement                   | Brace position |
|-----------------------------|----------------|
| Namespace                   | same line      |
| Type                        | same line      |
| Method (including ctor)     | **new line**   |
| Properties                  | same line      |
| Control blocks (if, for...) | same line      |
| Anonymous types and methods | same line      |

Multiline Parameters
--------------------

When you need to write down parameters in multiple lines, indent the parameters to be below the previous line parameters, like this:

Good:

``` csharp
WriteLine (format, foo,
           bar, baz);
```

If you do not want to have parameters in the same line as the method invocation because you ar running out of space, you can indent the parameters in the next line, like this:

Good:

``` csharp
WriteLine (
       format, moved, too, long);
```

Comma separators go at the end, like a good book, never at the beginning:

Good:

``` csharp
WriteLine (foo,
           bar,
           baz);
```

Atrocious:

``` csharp
WriteLine (foo
           , bar
           , baz);
```

Use whitespace for clarity
--------------------------

Use white space in expressions liberally, except in the presence of parenthesis:

good:

``` csharp
if (a + 5 > method (blah () + 4))
```

bad:

``` csharp
if (a+5>method(blah()+4))
```

File headers
------------

For any new files, please use a descriptive introduction, like this:

``` csharp
//
// System.Comment.cs: Handles comments in System files.
//
// Author:
//   Juan Perez (juan@address.com)
//
// Copyright (C) 2002 Address, Inc (http://www.address.com)
//
```

If you are modyfing someone else's code, and your contribution is significant, please add yourself to the Authors list.

Multiline comments
------------------

For long, multiline comments use either:

``` csharp
/*
 * Blah
 * Blah again
 * and another Blah
 */
```

Or:

``` csharp
//
// Blah
// Blah again
// and another Blah
//
```

Casing
------

Argument names should use the camel casing for identifiers, like this:

good:

``` csharp
void Method (string myArgument)
```

bad:

``` csharp
void Method (string lpstrArgument)
```

``` csharp
void Method (string my_string)
```

(There is an exception to this rule: [Gtk#](/docs/gui/gtksharp/) codebase, in which you should use under_score.)

Instance fields should use underline as a separator:

good:

``` csharp
class X {
     string my_string;
     int    very_important_value;
}
```

passable:

``` csharp
class X {
      string myString;
      int    veryImportantValue;
}
```

bad:

``` csharp
class X {
      int      _intval;
      string   m_string;
}
```

The use of "m\_" and "\_" as prefixes for instance members is highly discouraged.

An exception to this rule is serializable classes. In this case, if we desire to have our serialized data be compatible with Microsoft's, we must use the same field name.

this
----

The use of "this." as a prefix in code is discouraged, it is mostly redundant. In general, since internal variables are lowercase and anything that becomes public starts with an uppercase letter, there is no ambiguity between what the "Foo" and "foo" are. The first is a public property or field, the second is internal property or field.

Good:

``` csharp
class Foo {
    int bar;
 
    void Update (int newValue)
    {
       bar = newValue;
    }
 
    void Clear ()
    {
       Update ();
    }
}
```

Bad:

``` csharp
class Foo {
    int bar;
 
    void Update (int newValue)
    {
       this.bar = newValue;
    }
 
    void Clear ()
    {
       this.Update ();
    }
}
```

An exception is made for "this" when the parameter name is the same as an instance variable, this happens sometimes in constructors or if naming is difficult:

Good:

``` csharp
class Message {
     char text;
 
     public Message (string text)
     {
         this.text = text;
     }
}
```

Line length and alignment
-------------------------

Line length: The line length for C# source code is 180 columns (Used to be 80).

If your function declaration arguments go beyond this point, please align your arguments to match the opening brace. For best results use the same number of tabs used on the first line followed by enough spaces to align the arguments. That ensures that the arguments will remain aligned when viewed with a different tabsize. In the following example, the line that declares argc is indented with 2 tabs and 15 spaces:

``` csharp
namespace N {
    class X {
        void Function (int arg, string argb,
                       int argc)
        {
        }
    }
}
```

When invoking functions, the rule is different, the arguments are not aligned with the previous argument, instead they begin at the tabbed position, like this:

``` csharp
void M ()
{
    MethodCall ("Very long string that will force",
        "Next argument on the 8-tab pos",
        "Just like this one");
}
```

Initializing Instances
----------------------

Use the new C# syntax to initialize newly created objects.

Bad:

``` csharp
     var x = new Foo ();
     x.Label = "This";
     x.Color = Color.Red;
```

Good:

``` csharp
     var x = new Foo () {
         Label = "This",
         Color = Color.Red
     };
```

Baroque Coding
--------------

Baroque coding is discouraged.

We discourage the use of the "private" keyword to flag internal fields or methods since this is the default visibility mode in C#. The keyword exists because of Java. Avoid it, it merely is more line noise for people that are reading your code.

But the same principle applies everywhere else in Mono. Avoid complex code or redundant code for the sake of it. Try to write the minimum amount of text possible.

Warnings
--------

Avoid commiting code with warnings to the repository, the use of #pragmas to disable warnings is strongly discouraged, but can be used on unique cases. Please justify the use of the warning ignore clause on a comment.

Do not commit changes to the Makefiles that removes warnings, if anything warnings should be eliminated one at a time, and if not possible, they must be flagged.

Conditional compilation
-----------------------

Ideally we would not need conditional compilation, and the use of #ifdef is strongly discouraged. But due to our support for old C# 1.0 compilers we have to use it in a few places.

Try to avoid negative tests that have an else clause, for example:

``` csharp
            #if !NET_2_0
                CODE_FOR_1_0
            #else
                CODE_FOR_2_0
            #endif
```

Instead use:

``` csharp
            #if NET_2_0
                CODE_FOR_2_0
            #else
                CODE_FOR_1_0
            #endif
```

When a major feature differs across compilation targets, try to factor out the code into a separate class, a helper class or a separate file, and include that in your profile while surrounding that helper file/class with the ifdefs to reduce the amount of ifdefs in the code.

For instance, this is used for some parts of Grasshopper where the code is ifdefed out, when large parts of a file would have been ifdefed out, we moved the code into a MyOtherFile.jvm.cs

For 2.0 classes, this is even simpler as code can be trivially factored out into

    MyHelperClass.cli.cs
    MyHelperClass.jvm.cs

By using partial classes.

Missing Implementation Bits
---------------------------

There are a number of attributes that can be used in the class libraries to flag the specific state of an API, class or field.

The following attributes exist:

MonoDocumentationNote, MonoExtension, MonoInternalNote, MonoLimitation and MonoNotSupported.

If you implement a class and you are missing implementation bits, please use the attribute MonoTODO. This attribute can be used to programatically generate our status web pages:

``` csharp
[MonoTODO ("My Function is not available on Mono")]
int MyFunction ()
{
        throw new NotImplementedException ();
}
```

Ideally, write a human description of the reason why there is a MonoTODO, this will be useful in the future for our automated tools that can assist in developers porting their code.

Do not use MonoTODO attributes for reminding yourself of internal changes that must be done. Use FIXMEs or other kinds of comments in the source code for that purpose, and if the problem requires to be followed up on, [file a bug](/community/bugs/).

NotImplementedException
-----------------------

In the Mono class libraries, if a library is stubbed out, it is customary to insert the following code snippet:

``` csharp
    throw new NotImplementedException ()
```

The NotImplemented exception is used by tools like the [Mono Migration Analyzer](/docs/tools+libraries/tools/moma/) (Moma) to report potential problems for people porting their applications.

Notice that in certain conditions, throwing a NotImplementedException is a pattern used in base virtual methods to force derived classes to implement the functionality. This can lead to incorrect reports from the Moma tool, because the tool has no way of knowing that in practice the virtual base method will never be called (it would be better to have an abstract class in this case, but we have to be source and binary compatible). In these cases, instead of throwing the exception directly, call a helper routine, so that it becomes invisible to Moma:

``` csharp
Exception GetNotImplemented ()
{
     return new NotImplementedException ();
}
 
void SomeMethod ()
{
     throw GetNotImplemented ();
}
```

Remember the rule: NotImplementedExceptions should be exposed in the toplevel method that is exposed to developers for Moma to properly work.

Use of var
----------

Use var on the left-hand side of an assignment when the type name is repeated on the right hand side:

bad:

``` csharp
    NSUuid monkeyUUID = new NSUuid (uuid);
```

good:

``` csharp
    var monkeyUUID = new NSUuid (uuid);
    NSUuid something = RetrieveUUID ();
```

Use Simple Identifiers
----------------------

Use simple identifiers when possible.

passable:

``` csharp
var speechSynthesizer = new AVSpeechSynthesizer ();
var speechUtterance =
  new AVSpeechUtterance ("Shall we play a game?");
speechSynthesizer.SpeakUtterance (speechUtterance);
```

delightful:

``` csharp
var synthesizer = new AVSpeechSynthesizer ();
var utterance = new AVSpeechUtterance ("Shall we play a game?");
synthesizer.SpeakUtterance (utterance);
```

Examples
--------

``` csharp
class X : Y {
    bool Method (int argument_1, int argument_2)
    {
        if (argument_1 == argument_2)
            throw new Exception (Locale.GetText ("They are equal!");
 
        if (argument_1 < argument_2) {
            if (argument_1 * 3 > 4)
                return true;
            else
                return false;
        }
 
        //
        // This sample helps keep your sanity while using 8-spaces for tabs
        //
        VeryLongIdentifierWhichTakesManyArguments (
            Argument1, Argument2, Argument3,
            NestedCallHere (
                MoreNested));
    }
 
    bool MyProperty {
        get {
            return x;
        }
 
        set {
            x = value;
        }
    }
 
    void AnotherMethod ()
    {
        if ((a + 5) != 4) {
        }
 
        while (blah) {
            if (a)
                continue;
            b++;
        }
    }
}
```

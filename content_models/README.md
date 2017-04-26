# Content Modeling

A Google search for `digital preservation "content model"` will bring up a world of relevant and informative results, but a single definition for "content model" does not emerge.

For the purposes of this documentation, a working definition for "content model" is proposed:

> Content Models are opinionated blueprints for how an abstract, intellectual item, such as a photograph or a book, is represented as digital files within a digital object repository to support preservation and access.

## What?

Many modern digital object repository software allow you to "model" your content in any form you wish.  This is both a blessing and curse.

A **blessing**, because it allows for ultimate flexibility and extensibility.  When systems are too prescriptive, it may inhibit adding new kinds of content, or new derivative forms of an object.  But when a system allows you to model content, it allows for greater control of preservation workflows and options for access.

A **curse**, because the system has no "opnion."  If you have digitized a book with 100 pages, you might have:

 * 100 TIFF images for each
 * 100 PDFs for each page  
 * 100 XML files for each page with word locations
 * 100 TXT files for the raw text from each page

How do you organize these 400 files that represent a *single* book in your repository?  Do you lump them all together in a "bag" of files?  Do you create a sperate digital object for each page?  The options are limitless!

The answer is **content modeling**: creating a set of rules and organizational structure for how complex digital objects will be preserved in your system, which will also determine how those materials are searched and retrieved.

## WSUDOR Content Modeling

This section of the documentation includes specifics for how content is modeled in the Wayne State University's Digital Object Repository (WSUDOR) platform.

 1. [overview of Intellectual vs. Fedora Objects](fedora_objects.md)
 2. [overview of WSUDOR Content Models](wsudor_content_models.md)



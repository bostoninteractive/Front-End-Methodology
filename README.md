1. [Background](#boston-interactive-front-end-methodology-and-standards)
  * [Justification](#justification)
  * [Goals](#goals)
    * [Definition of good CSS (*Intra*-Team Goals)](#definition-of-good-css-intra-team-goals)
    * [Benefits of good CSS (*Inter*-Team Goals)](#benefits-of-good-css-inter-team-goals)
2. [Component Class Naming Conventions](#component-class-naming-conventions)
  * [Overview](#overview)
  * [Foundation naming convention](#foundation-naming-convention)
3. [Identifying components](#identifying-components)
4. [Formatting](#formatting)
5. [File structure](#file-structure)
6. [Approach](#approach)
  * [Leverage HTML elements](#leverage-html-elements-to-their-fullest-extent)
  * [Deliverable is a set of components](#deliverable-is-set-of-components-never-templates)
7. [Foundation Framework](#foundation-framework)
8. [SASS](#sass) 
9. [Getting Started](#getting-started)

# Boston Interactive Front End Methodology and Standards

## Background

### Justification
There are many (many) documented front methodologies; each with their strengths
and each with their shortcomings. We have found that no one methodology covers
all aspects or all scenarios that we at Boston Interactive need addressed.

This isn't because the existing documents are flawed. It has more to do with
the scope of each document - either covering too much or, in some cases, too
little. Either way, we couldn't find a definitive document that covered all of
our needs. Nor could we find a set of documents that covered our needs without
that set overlapping or contradicting itself.

### Goals
**Efficiency while producing a great deliverable is the ultimate goal.** The
sub-goals that will help us achieve that follow:

* Avoid pixel pushing layout issues
* Leverage frameworks to their fullest extent
* Compartmentalize code by function

#### Definition of good CSS (*Intra*-Team Goals)
* **Predictable**  
  Good CSS should be predictable. When a class is added or removed to an
  element, the developer should be able to accurately predict what effect that
  class's rules will have on the element.

* **Reusable**  
  Developers shouldn't have to write a new rule to, for example, float an
  element to the left. They should be able to reuse a float class, usually
  provided by the framework. Similarly, a developer shouldn't have to repeatedly
  set the background color of elements. There should be a single, reusable
  class for each background color.

* **Maintainable**  
  The addition of new components and features should not require the developer
  to re-factor existing CSS. New components and features should also make use of
  existing CSS to the fullest extent. Often, after careful study, new
  components are found to actually be variations on existing components that
  can be developed using modifier classes exclusively.

* **Scalable**  
  Scalable refers more to the size of the team than the size of the project.
  CSS that is scalable is easily approached by a new developer without a long
  ramp-up period. The CSS should make intuitive sense to the developer after an
  initial inspection.

#### Benefits of good CSS (*Inter*-Team Goals)

* **Backend handoff**  
  Backend developers are just that: Back End Developers. They shouldn't need to
  massage your CSS to make it work within the Content Management System. Their
  primary concern is the CMS itself. In many circumstances, the back-end
  developer won't have full control of the HTML that is generated by the CMS
  (or modifying the HTML will be prohibitively complicated). Good CSS is more
  easily integrated into a CMS.

* **Client approval**  
  Good CSS is inherently less buggy. This means that producers will encounter
  less surprises during integration, content entry, and QA. Even when bugs are
  easily understood and fixed, their presence can affect a clients confidence
  and can lead to additional requests and work.

## Component Class Naming Conventions

### Overview
The majority of CSS classes will be used to define components, define elements
of those components, or to modify those components or their elements. Use
patterns first proposed by BEM (Block, Element, Modifier) to distinguish between these three type of classes.  In our case we will use Component instead of Block. 

1. **Component**  
   Name of the component. If component is more than one word long, use a single
   hyphen to separate the words. For example:

    .tile

2. **Element**  
   Name of the component to which the element belongs, followed by two hyphens,
   followed by the element name. If the element name is more than one word
   long, use a single hyphen to separate the words. For example:

    .tile--body

3. **Modifier**  
   Name of the component that is being modified, followed by two underscores.
   followed by a description of the modifier. If the modifier is more than one
   word long, use a single hyphen to separate the words. You can also modify
   component elements by appending two underscored to the Component/Element
   combo followed by a description of the modifier. For example:

   .tile__large
   .tile--body__squeezed

### Foundation Naming Convention
You'll notice that Foundation does *not* follow these naming conventions; which
might seem counterintuitive at first. For example, Foundation provides classes
such as `.text-left` and .`text-right`. According to our method, those
should be named `.text__left` and `.text__right` respectively.

However, this apparent conflict actually allows us to easily distinguish
between classes provided by the framework and classes that are project
specific. When modifying components or adding elements to components provided
by the framework, the double underscore and double hyphen syntax should still
be used. 

## Identifying Components
One of the challenges of this approach is identifying what parts of a visual
design constitute a component. Indeed part of the goal of using these naming
conventions is to force the developer to take a step back and break a visual
design into its components.

For some projects, the developer might be lucky enough to be involved in this
process from the content strategy phase. In these cases, components will likely
follow content and content presentation requirements (which are discovered with
the UX team). In most cases, however, it will be up to the developer to
identify the components from an already finished design. Some tips to aid in
this process:

1. **Step away from the designs.**  

2. **Involve the design and UI teams.**  

3. **Identify which components might lend themselves to components already
   provided by the framework.**  

4. **Where appropriate, simplify.**  

## Formatting
* One space between the selector and the opening curly brace.
* Property:value pairs are each on their own line with two leading spaces.
* Property:value pairs are alphabetized by property per selector.
* Closing curly brace is on its own line with no spaces.
* Comments follow the doxegen format. Use double slash comments in SASS for
  comments that shouldn't be visible in compiled CSS.

## File Structure
Each section of the document has it's own partial seperated out to improve developer experience.

1. **Base**  
   The Base stylesheet contains almost exclusively single element selectors; but it could include attribute selectors, pseudo-class selectors, child selectors or sibling selectors. Essentially, a base style says that wherever this element is on the page, it should look like this.
   
   Base can also be used for basic styles that don't map well to HTML elements.
   For example, you might have background color classes in this file.

2. **Components**  
   This is your main style sheet. It should be readable by a human and heavily
   commented. Each component and its elements and modifiers should be logically
   grouped and seperated by a comment describing the component, how it
   interacts with other components, and how it can be modified.

3. **Elements**
   Styles for your HTML elements go here. For example, body and header styles. 

4. **Mixins**
   Mixins allow us to create reuable groups of CSS. This helps us aviod writing repetitive code. In the below example we created a 'border-radius' mixin. 
    
    @mixin border-radius($radius) {

        -webkit-border-radius: $radius;
           -moz-border-radius: $radius;
            -ms-border-radius: $radius;
                border-radius: $radius;          
    
    }
 
    .box {

      @include border-radius(10px); 
    
    }


5. **Fonts**

6. **Header**

7. **Footer**


## Approach

### Leverage HTML elements to their fullest extent
It\'s often useful to start by defining the layout and look of each HTML
element before diving into components. If the designer hasn't provided these
styles, ask for them. Then, make sure that components don't unnecessarily
deviate from those styles.

For example, if `h3` is defined as `font-size: 24px`
and `h4` is defined as `font-size: 20px`, the heading of a `panel` component
should leverage one of those two styles rather than defining its own. (E.g., the
designer shouldn't define panel headings at 22 pixels - which would be between
the h3 and h4 definitions.)

The same applies for layout rules. If an `h1` has 20 pixels of bottom margin,
the designs shouldn't show an element less than 20 pixels below any `h1`
anywhere on the site. If you find cases of this, bring them to the attention of
the designer.

### Deliverable is set of components, never templates
This doesn\'t necessarily mean that you won\'t deliver a page of components to
help the back-end dev get started. But you should never approach the project as
a set of templates.

Once components are identified, it helps to break them down into elements and then identify how the components and their elements can be modified. Sometimes, writing these components, their elements, and how they can be modified out in the hierarchical notation of your choice helps.


## Foundation Framework 

Our responsive front-end framework of choice is foundation. 
https://foundation.zurb.com/sites/docs/index.html

A good place to start when identifying components is the kitchen sink page:
https://foundation.zurb.com/sites/docs/kitchen-sink.html

## SASS 

For a preprocessor we use SASS. For more information on SASS see: http://sass-lang.com/guide


## Getting Started 

We have boilerplates for both Kentico and Drupal sites, both include the foundation framework and SASS files. https://github.com/bostoninteractive/bi-boilerplate

For Kentico Sites:

  Use the kentico-frontend branch and copy the 'starter-theme' files to your project

  Use the 'kentico-kitchensink' for reference of our coding style and some common components. 


For Drupal Sites: 


Use the master branch '/D8_foundation_master/zurb_foundation/STARTER/' theme

The most direct way to get up and running with a SASS compiler is using your terminal. 

Simply cd into your theme directory and run the below commands:  

 
   npm install


   bower install


   npm start






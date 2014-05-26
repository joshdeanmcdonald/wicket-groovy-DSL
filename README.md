#Apache Wicket Groovy DSL Project

## Overview
Apache Wicket is great, and Groovy is also great. This project tries to combine the power of both. However, sometimes Apache Wicket code become damn verbose.
But with some little, yet powerful Groovy DSL written, we can extend Wicket to simplify common tasks, and to delete over 30-40% of verbose code.
Versions used:
### 1. Apache Wicket 6.15.0
### 2. Groovy 2.3.1 (Yes, with Traits :)
### 3. Twitter bootstap for some beautify

## Pimp my library pattern
This project follows Pipm my library pattern described by Martin Odersky in 2006 year. The Pimp my Library Pattern suggests an approach for extending a library that nearly does everything that you need but just needs a little more. It assumes that you do not have source code for the library of interest.
Read more here: http://groovy.codehaus.org/Pimp+my+Library+Pattern

## Examples
Later I will provide more complex examples. But to understand the concept, I think it is enough.
At this moment Label, AjaxLink, MarkupContainer, Form, StatelessForm, ListView, Link, BookmarkableLink, PasswordField, TextField are implemented

##Usage
```groovy
...
use(WicketDSL, WicketFormDSL) {
    def form = form 'wicketForm', new CompoundPropertyModel(this),
    [ submit: { println this.input1 + this.input2 },
      visible: { this.input1 != this.input2 } ]

    form.field 'input1'
    form.field 'input2'
    ['one', 'two', 'three'].listView('listView') { ListItem item ->
        item.label 'itemLabel', item.model
    }
}
```
Instead of
```java
...
   Form form = new Form("wicketForm", new CompoundPropertyModel(this)) {
        @Override
        public void onSubmit(){
            System.out.println(MyPage.this.input1 + MyPage.this.input2);
        }
        @Override
        public boolean isVisible() {
            // just for example :)
            !MyPage.this.input1.equals(MyPage.this.input2);
        }
   }
   form.add(new TextField("input1"));
   form.add(new TextField("input2"));
   add(form);
   ArrayList<String> list = new ArrayList<>();
   list.add("one"); list.add("two"); list.add("three");
   add(new ListView("listView", list) {
        @Override
        protected void populateItem(ListItem<T> item) {
            item.add(new Label("itemLabel", item.getModel()));
        }
   })
```

And this is just a small example of usage. Also with an override map (in this example with 'submit' key), you can pass another properties to components, like
visible, enabled and others (take a look at traits wicket/core/traits package).

##Thanks

Thanks to great Groovy Community, and especially to Andrey Bloschetsov.
Also thanks to Martin Dashorst, for providing post about this project at http://wicketinaction.com

##Development
DSL is not complete, it is just the attempt to show you the concept.
Feel free to contact me, to advise me how to make this DSL better.

##Help
I need help in testing this DSL, also I need your opinion on this
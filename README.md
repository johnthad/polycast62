# Asynchronous Actions with Redux and Polymer 2

Rob Dodson's [Polycast #62](https://www.youtube.com/watch?v=y2FxAT1u8pU) demonstrated how to use Redux with async actions in Polymer 1.X. I have adapted his lesson for Polymer-2.0-rcX.

In order to do things the Polymer 2 way, I am also using the polymer-2 branch of [Polymer Redux](https://github.com/tur-nr/polymer-redux).

The tricky part of this revision was using two behaviors/mixins in `sign-up-form.html`. My solution was changing `AsyncActionsBehavior` in `redux-store.html` to a mixin that returns a class expression (see my `AsyncActionsMixin`). Then (in `sign-up-form.html`) `AsyncActionsMixin` extends `Polymer.Element` to create `ThunkMixin`, and `ReduxMixin` extends `ThunkMixin` to create `SignUpForm`. (Is there a better approach? Comments welcome.)

## Revised mixin

After reading an excellent [post on mixins](http://justinfagnani.com/2015/12/21/real-mixins-with-javascript-classes/) by Justin Fagini, I realized that I could tighten `SignUpForm`'s declaration from

    class ThunkMixin extends AsyncActionsMixin(Polymer.Element) {};

    class SignUpForm extends ReduxMixin(ThunkMixin) {...

to

    class SignUpForm extends ReduxMixin(AsyncActionsMixin(Polymer.Element)) {

And so that is how you see `sign-up-form.html` now.

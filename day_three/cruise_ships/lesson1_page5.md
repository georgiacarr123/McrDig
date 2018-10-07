:twisted_rightwards_arrows: **Driver and Navigator switch roles if you haven't already done so**

Feel free to switch roles as often as you see fit for this part of the walkthrough.

## I don’t want my ship to dock at a port if the port is full

```
As a ship captain,
So I can dock my ship,
I don’t want my ship to dock at a port if the port is full.
```

## Ports have capacity

Our user story states that a port can be full. This creates a problem for us as it means ports now need to know which ships are docked with them. 

1. In `PortSpec.js` in the `describe` callback, declare a new variable `ship`, and inside the `beforeEach` callback, assign a new instance of the `Ship` object to `ship` passing in `port`:

```js
  let weather;
  let port;
  let ship;

  beforeEach(function () {
    weather = new Weather();
    port = new Port(weather);
    ship = new Ship(port);
  });
```

2. Add a new test `can add ships`:

```js
it('can add ships', function () {
  
});
```

3. Call `add` on `port`, passing in `ship`, and then `expect` `port.getShips()` `toContain` `ship`:

```js
it('can add ships', function () {
  port.addShip(ship);

  expect(port.getShips()).toContain(ship);
});
```

4. Run the tests. You should fail with the error `TypeError: port.addShip is not a function`. Go ahead and create the `addShip` method to get rid of the error.

5. Run your tests again. You should now fail with the error `TypeError: port.getShips is not a function`.

6. Create the `getShips` method (but don't write any more than you need to - just enough to pass the error).

7. Run your tests. The error you should now have is: `Expected undefined to contain Object({ _currentPort: Object({ _weather: Object({ _NOT_STORMY_PROBABILITY: 0.5 }) }) }).`. We can now go ahead and write the code to pass our failing test.

8. Our `Port` can have multiple ships, so it makes sense to store these in an array on the `Port` constructor. Add a new property to `Port` named `_ships` and assign to it an empty array.

9. Now inside your `getShips` method, return the value of your `_ships` property.

10. Run your tests. They should still fail - now with the error: `Expected [  ] to contain Object({ _currentPort: Object({ _weather: Object({ _NOT_STORMY_PROBABILITY: 0.5 }), _ships: [  ] }) }).`. 

11. Before, our `getShip` method was returning `undefined` and now it's returning an empty array. The reason the array is still empty is because we haven't actually put a ship in it yet. We can see from our test that `addShip` takes a `ship` so go ahead and add the code to that method that adds `ship` into the `_ships` array.

12. Now run your tests. If you've done everything correctly, you should now be passing.

## A ship docks, a port adds the ship

Think about a ship in real life. It sails itself to the port - the port doesn't pull it in. Our `Port` still has to keep track of the `Ship` though. Therefore, when our `Ship` is ready to `dock` at the port, we need to instruct the `Port` to add our `Ship` to its records. We could do this manually, but it'd be much more user-friendly if adding te `Ship` to the port was  handled automatically for us, as its something we'll always need to do when we `dock` a ship.

Put simply, when we call `ship.dock()`, we need to also call `addShip` on the `Port` we are docking at. And to test this, we need to spy on `Port`'s `addShip` method from our `Ship` test.

1. Inside `ShipSpec.js` create a new test `is instructs the Port to add the ship`:

```js 
it ('instructs the Port to add the ship', function () {

});
```

2. Now we want to `spyOn` `arrivalPort`'s `addShip` method: 

```js
it('instructs the Port to add the ship', function () {
  spyOn(arrivalPort, 'addShip')
})
```

Jasmine will now listen in on `arrivalPort.addShip()`.

2. Now call the `dock` method on `ship` and pass in `arrivalPort` as the only argument:

```js 
it('instructs the Port to add the ship', function () {
  spyOn(arrivalPort, 'addShip');

  ship.dock(arrivalPort);
})
```

3. Finally, we want our assertion. Call `expect` and pass in `arrivalPort.addShip`. Then on the `expect`'s returned object, call the `toHaveBeenCalledWith` method and pass in `ship`:

```js 
it('instructs the Port to add the ship', function () {
  spyOn(arrivalPort, 'addShip');

  ship.dock(arrivalPort);

  expect(arrivalPort.addShip).toHaveBeenCalledWith(ship);
});
```

***
:bulb:

First of all here with `spyOn(arrivalPort, 'addShip')`, we tell Jasmine to listen in (*spy*) on an object's method (`arrivalPort.addShip()`). It will keep spying on this method until the test has finished.

Then we go ahead and ready ourselves for the assertion. We call `ship.dock(arrivalPort)`. Our spy is still listening, whilst this method executes.

Finally, we make an assertion the method we're spying on that it has been called (with an argument): `expect(arrivalPort.addShip).toHaveBeenCalledWith(ship)`
***

4. Run your tests. We should be rightly failing again: `Expected spy addShip to have been called with [ Object({ _currentPort: Object({ _weather: undefined, _ships: [  ], addShip: spy on addShip }) }) ] but it was never called.`. Our test is telling us that it expect's the `arrivalPort`'s `addShip` method to have been called. 

The only piece of our application's code we run in our test is `ship.dock(arrivalPort)`, so the only way we can make this test pass it to call the `Port`'s `addShip` method inside of our `dock` method.

5. Inside `Ship.js`, find your dock method, and at the end call `addShip` on `port` and pass in `this` (the current instance of the ship):

```js
dock: function (port) {
  this._currentPort = port;

  port.addShip(this);
}
```

6. Run your tests. You should be green.

## Ports have capacity

"I don’t want my ship to dock at a port if the port is full."

Our port now knows what ships are docked in it, but it doesn't set a limit. We will say for the sake of this exercise that every port has a capacity of 8.

1. Inside your `PortSpec.js`, add a new test `has a capacity`.

2. `expect` `port.getCapacity()` `toBe` `8`.

3. Run the tests. The test `has a capacity` should fail. Use the top error of your stack trace to guide you, and go ahead and write the code to make the test pass.

:exclamation: Ask for your capacity code to be reviewed before you go any further!

## Full capacity!

4. Now inside `ShipSpec.js`, create a new test `doesn't dock if port at capacity`.

5. Inside your test's callback, `dock` a `ship` at a `port` 8 times (use a for loop to do this!). Your port will now be at capacity.

6. Now, still inside the callback, `expect` that when you `dock` a `ship` at a `port` it will throw an error `port is at capacity`.

7. Run your tests. This test should fail. Again, write the code to make the test pass (hint below).

***
:bulb:

This is a hard one. 

1. `getShips` that the `port` has.
2. Check if the adding 1 to the length of returned array *is greater than* the port's capacity.
3. If not then throw an error.
***

## Add, commit and push

[Summary](lesson1_summary.md)

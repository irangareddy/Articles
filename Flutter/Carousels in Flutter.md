# Carousels in Flutter

 Carousels are a great way to showcase different features of a product, advertise multiple products at once, or tell your brand story in chapters.

## What is a Carousel

A carousel is a Pin with multiple images and has a related short description for each image repectively which helps to convey context easily.

People see the carousel in their home feed just like any other Pin. They can swipe through the different images (or cards) directly from the feed. Or, they can tap on the Carousel and swipe through each card and its corresponding site, essentially swiping through the different landing pages.

### Let's Build a Carousels like this

<p align="center">
<a href="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/carouselCardsList.dart">
<img src="https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/Gifs/Carousels.gif?raw=true" width="250" alt="Context Menu" >
</a>
</p>

This is actually what we going to make by the end of this article. Load up your energy and let's get started.

### Model Class

```dart
class TeslaCar {
  TeslaCar({this.model, this.image, this.description});

  String model;
  String image;
  String description;
}
```

We are going to creating a Tesla Car Carousel so we need to create a Model Class like above

- `model` which describes the Model of the Car.
- `image` will have a `NetworkImage` Url link of the Car.
- `description` provides the description of the Car.

### Array of Cars

```dart
var cars = [
  TeslaCar(
      model: 'Roadster',
      image: 'https://wallpaperaccess.com/full/1152734.jpg',
      description:
          'As an all-electric supercar, Roadster maximizes the potential of aerodynamic engineering—with record-setting performance and efficiency.'),
  TeslaCar(
      model: 'Model S',
      image: 'https://wallpapershome.com/images/pages/pic_v/8763.jpeg',
      description:
          "Model S sets an industry standard for performance and safety. Tesla’s all-electric powertrain delivers unparalleled performance in all weather conditions."),
  TeslaCar(
      model: 'Model 3',
      image: 'https://wallpapershome.com/images/pages/ico_v/20707.jpg',
      description:
          "Model 3 comes with the option of dual motor all-wheel drive, 20” Performance Wheels and Brakes and lowered suspension for total control, in all weather conditions."),
  TeslaCar(
      model: 'Model X',
      image:
          'https://images.hdqwalls.com/download/tesla-model-x-front-4k-5x-1080x1920.jpg',
      description:
          "Tesla’s all-electric powertrain delivers Dual Motor All-Wheel Drive, adaptive air suspension and the quickest acceleration of any SUV on the road—from zero to 60 mph in 2.6 seconds."),
  TeslaCar(
      model: 'Model Y',
      image:
          'https://www.autocar.co.uk/sites/autocar.co.uk/files/images/car-reviews/first-drives/legacy/model_y_front_34_blue.jpg',
      description:
          "Tesla All-Wheel Drive has two ultra-responsive, independent electric motors that digitally control torque to the front and rear wheels—for far better handling, traction and stability."),
  TeslaCar(
      model: 'Cyber Truck',
      image: 'https://img.wallpapersafari.com/phone/750/1334/65/24/BAlZne.jpg',
      description:
          "The powerful drivetrain and low center of gravity provides extraordinary traction control and torque—enabling acceleration from 0-60 mph in as little as 2.9 seconds."),
];
```

We need an array of Cars for Coursels which are created using `TeslaCar` Class

### Carousel Card

```dart
// ignore: must_be_immutable
class CarouselCard extends StatelessWidget {
  CarouselCard({this.car});

  TeslaCar car;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Padding(
        padding: EdgeInsets.only(
          top: 32.0,
          left: 8.0,
          right: 8.0,
        ),
        child: Container(
          width: MediaQuery.of(context).size.width * 0.7,
          height: MediaQuery.of(context).size.height * 0.5,
          decoration: BoxDecoration(
            // color: Colors.redAccent,
            borderRadius: BorderRadius.circular(16.0),
            boxShadow: [
              BoxShadow(
                  color: kShadowColor, offset: Offset(0, 20), blurRadius: 10.0),
            ],
            image: DecorationImage(
                image: NetworkImage(car.image), fit: BoxFit.cover),
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Container(
                  width: 44,
                  height: 44,
                  child: Image.network(
                    'https://upload.wikimedia.org/wikipedia/commons/thumb/b/bd/Tesla_Motors.svg/595px-Tesla_Motors.svg.png',
                    fit: BoxFit.contain,
                  ),
                ),
              ),
              Spacer(),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: Row(
                  children: <Widget>[
                    Spacer(),
                    Column(
                      crossAxisAlignment: CrossAxisAlignment.end,
                      children: <Widget>[
                        Text(
                          car.model,
                          style: kCardTitleStyle,
                        ),
                        Container(
                          height: 100,
                          width: MediaQuery.of(context).size.width * 0.6,
                          child: Text(
                            car.description,
                            style: kCardDescriptionTextStyle,
                            textAlign: TextAlign.end,
                            overflow: TextOverflow.ellipsis,
                            maxLines: 5,
                          ),
                        ),
                      ],
                    ),
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

We need a Carousel Card before creating a Carousel List So, follow below steps to create a  Carousel Card like above

- Create a Stateless widget name it as `CarouselCard`
- Declare a variable `car` of type `TeslaCar` because we are going pass `TeslaCar` object to get properties of the car
- Create a `Container` with height and width properties. (Use your custom height and width, I used MediaQuery because these will be adjusted according to the `screensize`)
- `decoration` is the property where we are going to give a `borderRadius`, `boxShadow` and `image` of the Card
- In the `child` property we are going to rest of the things like `Tesla logo`, `model` name and `description` of the Car

### Coursel List

```dart
class CarouselList extends StatefulWidget {
  @override
  _CarouselListState createState() => _CarouselListState();
}

class _CarouselListState extends State<CarouselList> {
  int currentPage = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: kPrimaryColor,
        title: Text("Carousels"),
        centerTitle: false,
      ),
      body: Column(
        children: <Widget>[
          Spacer(),
          Container(
            height: MediaQuery.of(context).size.height * 0.6,
            width: double.infinity,
            child: PageView.builder(
              itemBuilder: (context, index) {
                return Opacity(
                  opacity: currentPage == index ? 1.0 : 0.8,
                  child: CarouselCard(
                    car: cars[index],
                  ),
                );
              },
              itemCount: cars.length,
              controller:
                  PageController(initialPage: 0, viewportFraction: 0.75),
              onPageChanged: (index) {
                setState(() {
                  currentPage = index;
                });
              },
            ),
          ),
          updateIndicators(),
          Spacer(),
          Column(
            children: <Widget>[
              Text('Flutter UI Component Library',style: kHeadlineLabelStyle,),
              Text('@irangareddy',style: kSubtitleStyle,)
            ],
          ),
          Spacer(),
        ],
      ),
    );
  }
}
```

 We have successfully created a `CarouselCard` but we need to create a `List` before we actually witness the `Coursels`

- Create a `Stateful Widget` and name it as `CourselList`.(You will shortly know, why we are created a StatefulWidget)

- Create a `Container` and give a `height > CarouselCard height` and `width = double.infinity` because, we know the `height` of the Card but don't know how much `width` occupies for list of the `Cards`

- Here comes the important area `child` property, we are declaring a `PageView`

**Important**: About PageView(Skip if you know)

- A `PageView` is almost like Lists but, it works page by page. I am using this to build Horizontal List.

- Each child of a page view is forced to be the same size as the `viewport`.

- You can use a `PageController` to control which page is visible in the view. In addition to being able to control the pixel offset of the content inside the PageView, a `PageController` also lets you control the offset in terms of pages, which are increments of the `viewport` size.

- The `PageController` can also be used to control the `PageController.initialPage`, which determines which page is shown when the PageView is first constructed, and the `PageController.viewportFraction`, which determines the size of the pages as a fraction of the viewport size.

*source: [Flutter API Docs](https://api.flutter.dev/flutter/widgets/PageView-class.html)*

These points give a clear idea of the PageView. I used this lines exactly form Docs because they are best.

Hope you got a exact idea of `PageView`

### Back to Building the Carousel

- With `itembuilder` property we are returning the `cards` of the list using `index` value
- Assign the array length to `itemCount`
- `controller` which manages view of the `PageView` using `PageViewController` and assign `initialPage` to `0`(starting point), `viewportFraction` is default set to 1 i.e, each card occupies whole view. Change the  `viewportFraction` to adjust the view.
- create a `currentPage` variable to know the current page of the PageView and update the value in `onPageChanged` property
- If you cleary observe the code we have an unimplemented `updateIndicators()` function

### Adding Indicators

```dart
  Widget updateIndicators() {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: cars.map(
        (car) {
          var index = cars.indexOf(car);
          return Container(
            width: 7.0,
            height: 7.0,
            margin: EdgeInsets.symmetric(horizontal: 6.0),
            decoration: BoxDecoration(
              shape: BoxShape.circle,
              color:
                  currentPage == index ? Colors.red : Color(0xFFA6AEBD),
            ),
          );
        },
      ).toList(),
    );
  }
```

This a Indicators widget which helps users to know *where they are* and *Total count of the Cards*

### Conclusion

Carousels convey context very fast and easy way to stick users with images and make advertise. Your can further extend this as Navigative ech card respective view and describing more about the context.

[GitHub Link](https://github.com/irangareddy/Flutter-UI-Components-Library/blob/master/lib/material/carouselCardsList.dart)

If you like to improve your App Development Skills, even more in Flutter and SwiftUI. Feel free to dm me on [Instagram](https://www.instagram.com/irangareddy/)  or tweet to me on [Twitter](https://twitter.com/irangareddy) if you have any additional tips or feedback.

Thanks for reading!

### Lofted B-spline surface interpolation



* [Lofted B\-spline surface interpolation](#lofted-b-spline-surface-interpolation)
* * [Extend the existing methods to closed contours](#extend-the-existing-methods-to-closed-contours)
  * [Programming](#programming)
  * [Lofting package](#lofting-package)
  * [Basic usage](#basic-usage)
  * [Demonstration of package](#demonstration-of-package)
    * [liver model](#liver-model)
    * [human head](#human-head)
    * [shoe model](#shoe-model)
    * [complex head](#complex-human-head)
    * [bottle model](#bottle-model)
    * [blade model](#blade-model)
    * [jaw model](#jaw-model)



#### Extend the existing methods to closed contours

The detailed procedures can be found from [this file](https://github.com/akka-like/LBSI/blob/main/method-extending.pdf)
s


#### Programming

We use the mixture of C and Wolfram language.



![C code](/assets/C-code-side.png)

![Wolfram language](/assets/wolfram-lang-side.png)

#### Lofting package

Lofting is a *Mathematica* package that implements some functionalities, like `LoftedInterpolate[]`, `LoftedApproximate[],` that associated with B-spline surface interpolation/approximation to serial rows of data points, where the number of data points varies from row to row. 

```mathematica
LoftedInterpolate[Q_ij, q, opts]

(* 
 returns a lofted B-spline surface interpolation for rows of data points Q_ij,
 where the number of each row varies from row to row. 
 
 q: row degree
 
 default options:
 {
   Method -> Automatic, 
   SplineClosed -> False, 
   "IntervalPercent" -> Automatic
 }
 
*)
```



#### Basic usage

Package and data points loading

```mathematica
(* load package *)
Needs["Lofting`"]

(* load data points *)
liverSections = Import[$ClosedPointSetPath <> "/liver_48_paper.xls"];
headSections  = Import[$ClosedPointSetPath <> "/head_92_paper.xls"];
shoeSections  = Import[$ClosedPointSetPath <> "/shoe_10.xls"];

```

Build surface from rows data points

```mathematica
(* build surface from data points *)

(* 
   SplineClosed: True / False
   Method      : "Piegl" / "Park"
*)
liverFunc2Park        = LoftedInterpolate[liverSections, 2, SplineClosed -> False, Method -> "Park"]
liverFunc2Piegl       = LoftedInterpolate[liverSections, 2, SplineClosed -> False, Method -> "Piegl"]
liverFunc2ParkClosed  = LoftedInterpolate[liverSections, 2, SplineClosed -> True,  Method -> "Park"]
liverFunc2PieglClosed = LoftedInterpolate[liverSections, 2, SplineClosed -> True,  Method -> "Piegl"]
```



#### Demonstration of package

##### liver model

![liver functions](/assets/liver-func.PNG)

![liver-points](/assets/liver-points.PNG)

![liver-surface](/assets/liver-surface.PNG)



##### human head

<img src="/assets/header-points.PNG" alt="header points" style="zoom:80%;" />

![Head surface](/assets/head-surface.PNG)



##### shoe model

![shoe points](/assets/shoe-points.PNG)

![Shoe surface](/assets/shoe-surface.PNG)



##### complex human head

![complex human head](/assets/complex-head-points.PNG)


![complex human surface](/assets/complex-head-surface.PNG)



##### bottle model

![bottle points](/assets/bottle-ctrlnet.png)



![bottle surface](/assets/bottle-surface.png)





##### blade model

![blade points](/assets/blade-points.PNG)



![blade surface](/assets/blade-surface.PNG)



##### jaw model

![jaw points](/assets/jaw-points.PNG)



![jaw surface](/assets/jaw-surface.PNG)
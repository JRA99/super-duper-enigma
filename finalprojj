import matplotlib.pyplot as plt
import matplotlib.path as mpath
import numpy as np
from pylab import rcParams
import math
from matplotlib.pyplot import figure

# Config for plot
color = 'k'
style = '.'
title = 'Generated Stress Vs. Strain Chart'

# a = 0
# b = float(input("What is the strain value at the yield point:"))
# bYpoint =float(input("Enter the stress value at %.3f :" %(b)))
# c = float(input("What is the strain value at the plastic-strainHardening point:"))
# cs =float(input("Enter the stress value at %.3f :" %(c)))
# d = float(input("What is the strain value at the point of maximum strength:"))
# ds =float(input("Enter the stress value at %.3f : " %(d)))
# e = float(input("What is the strain value at the fracture point :"))
# es =float(input("Enter the stress value at %.3f" %(e)))

# Implements test variables #todo remove after all tests
origin = 0
pointABx = 0.05
pointABy = 40.
pointCx = 0.12
pointCy = 40.
pointDx = 0.43
pointDy = 60
pointEx = 0.67
pointEy = 52
userAction = int(input(
    "To create a plot of the stress-strain curve enter [1], to input a strain value to output the stress value at that point enter [2]:"))


def f3(t):
    return ((pointDy - pointCy) / 2) * np.sin((1 / (np.pi * 0.1 * (pointDx - pointCx))) * (t - pointCx) - (np.pi / 2)) + pointDy - ((pointDy - pointCy) / 2)


def f4(t):
    return ((pointEy - pointDy) / 2) * np.sin((1 / (np.pi * 0.1 * (pointEx - pointDx))) * (t - pointDx) - (np.pi / 2)) + pointEy - ((pointEy - pointDy) / 2)


def deriv(x1, x2, y1, y2):  # takes derivative  as a slope, returns numerical derivative
    d_dt = 0
    d_dt = ((y2 - y1) / (x2 - x1))
    return d_dt


def stress(strain):  # defines function to calculate stress from strain
    str = 0
    if 0 <= strain < pointABx:
        str = deriv(0, pointABx, 0, pointABy)
    return str


if userAction == 1:
    # ----------------- B -------------------
    bx= np.linspace(0, pointABx)  # line ab
    db = deriv(0, pointABx, 0, pointABy)
    by = bx * db

    plt.plot(0, 0, color + style)
    plt.plot(bx, by, color)  # plots ab
    plt.plot(pointABx, pointABy, color + style)  # plot point b


    # ----------------- C -------------------
    cx = np.linspace(pointABx, pointCx)  # line ab-c

    dc = deriv(pointABx, pointCx, pointABy, pointCy)
    cy = dc * cx
    cy = cy + (pointABy - cy[0])

    plt.plot(pointCx, pointCy, color + style)  # plot point b
    plt.plot(cx, cy, color)
    # plt.annotate('Plastic Region', xy=(), xytext=(c - (c / 2), cs - (cs / 2)),  # Draws C and arrow
    #             arrowprops=dict(facecolor='black', shrink=0.05),
    #             )
    # ----------------- D -------------------
    dx = np.linspace(pointCx, pointDx)  # line ab-c
    #
    # dd = deriv(c,d,cs,ds)
    # dy = dd*dx
    # dy = dy + (cs-min(dy))
    #
    # plt.plot(d,max(dy),color+style) #plots point d
    # plt.plot(dx,dy,color)
    t3 = np.arange(pointCx, pointDx, .001)  # line ab-c
    plt.plot(t3, f3(t3), color)

    # ----------------- E -------------------

    ex = np.linspace(0, pointEx - pointDx)  # line ab-c
    # exx = np.linspace(d,e)
    # de = (es-ds)/(e-d)
    # ey = de*dx + ds
    # ey = ey + (ds-max(ey))
    t4 = np.arange(pointDx, pointEx, .001)

    plt.plot(t4, f4(t4), color)  # plots point d
    plt.plot(pointEx, pointEy, color + style)
    # -----------------PLOT------------------

    plt.title(title, fontsize=14, fontname='sans-serif')
    plt.grid(True, linestyle='-.')
    plt.xlabel('Strain [$\epsilon$]', fontsize=12)
    plt.ylabel(r'Stress [$\sigma$]', fontsize=12)
    plt.show()
elif userAction == 2:  # User wants to input strain for stress
    userInput = 1
    sout = 0
    while userInput >= 0:
        print("*** To exit, enter any negative number. ***")
        userInput = float(input("Enter a Strain value to calculate the corresponding stress value: "))
        if userInput < 0:
            break
        elif 0 < userInput <= pointABx:
            sout = deriv(0, pointABx, 0, pointABy) * userInput
        elif pointABx < userInput <= pointCx:
            sout = deriv(pointABx, pointCx, pointABy, pointCy) * userInput + pointABy
        elif pointCx < userInput <= pointDx:
            sout = deriv(pointCx, pointDx, pointCy, pointDy) * userInput + pointCy
        elif pointDx < userInput <= pointEx:
            sout = deriv(pointDx, pointEx, pointDy, pointEy) * userInput - pointEy
        else:
            print("The inputted strain value of %1.3f is past the breaking point of strain %1.3f" % (userInput, pointEx))
        print(sout)
else:
    print("Error - Invalid User Input.")

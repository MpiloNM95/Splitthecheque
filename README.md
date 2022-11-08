# Split_the_cheque app
## Simple Increment Counter App created using swift.
### Day 01 of learning IOS development through youtube projects:books:
* Learning the swift/swiftui and xcode through youtube first and with various projects while I have free time between full stack software engineering bootcamp.
* Enjoying the learning through projects from Youtube
* Will start the [100 Days of Swift](https://www.hackingwithswift.com/100) as well as the [100 Days of SwiftUI](https://www.hackingwithswift.com/100/swiftui)
* Currently following the Indently Youtube channel for the next swiftui/swift projects
---
### Functions of the app
* The app is desgined for a group of people being friends, asscociates, enemies, couples, functions. being business or family to split the cheque for a meal or at the pub or whatever the user deems useful.
* The app is split into 4 sections
* The first Section is for the amount before the tip percentage has been detereminde by the group 
* The second section is for the tip percentage which will be slected and decided between the group after said activity
* The third section is for the user to select how many people were in he/she group
* The forth section will be the amount that each member will pay after tip percentage has been factor in the currency of the country which in this case is South Africa for the Rand /ZAR.
### The code below: 
```
//
//  ContentView.swift
//  Splitthecheque
//
//  Created by Mpilo Mafu on 2022/11/08.
//

import SwiftUI

struct ContentView: View {
    // This is going to be the total the group of people pay
    // This called a private variable within swift
    @State private var totalCost = ""
    // This is another private variable which has been set to amout of people who have to pay for now
    @State private var people = 4
    // The 3rd variable will be for the tipindex
    // The tipIndex is for the user decide on which tipPercentage wiil be chosen depending on the user
    @State private var tipIndex = 2
    // Next variable will be for the tip percenatges
    // This is the list of the tip percentages which cn be selected
    let tipPercentages = [0, 5, 10, 15, 25]
    
    // This will be the function that calculates the final cost
    // In order to reduce errors must never forget to include the double or any function a the beginning
    func calculateTotal() -> Double {
        // We know have to specify a tip variabe
        // if the tip index is set at 2 then tipPercentage selected will be 10% which will then chane to a double
        let tip = Double(tipPercentages[tipIndex])
        // This is currently showing error due to totalCost still being set to "" strings instead of numbers for now.
        // The system cant turn letters in to numbers
        // If the user types anything but a number then the app wiil print out a zero cause the user hasnt typed out the number
        let orderTotal = Double(totalCost) ?? 0
        // This variable will calculate the amount the group should pay but not factor in the amount each person should pay
        let finalAmount = ((orderTotal / 100 * tip) + orderTotal)
        
        return finalAmount / Double(people)
    }
    // Now we are going to create the UI of the app
    // NavigationView will be for the different screens which move around  for the user
    var body: some View {
        NavigationView{
            // Inside the Form all the elements of the app will be included
            Form {
                // This is the header for the placeholder for the smount which is where the user will enter cheque amount
                Section(header: Text("Enter an amount")) {
                    // With the $ -> symbol we create a binding between @State totalCost as the app udates the state and the element will both update each other
                    // $ = Binding variable
                    // As soon as the user enters thee amount the normal keyboard with letters will come up
                    // To prevent that the keyboardType has been set to a decimalPad which means the numbers with the decimal system  will be avaliable for the user to enter
                    TextField("Amount", text : $totalCost).keyboardType(.decimalPad)
                }
                // This is the title for the tip element for the app
                Section(header: Text("Select a tip amount (%)")) {
                    // Picker is what will allow the user to chose the percentage for tip to be added tot the total amount for the group
                    // $tipIndecx it s binding variable for the tipIndex within the @State above
                    Picker("Tip percentage", selection: $tipIndex) {
                        // This means that the array of tipPercetages will be avaliable to be chisen by the user if not chosen the app will assume the amount for the tip to be 0 = no tip
                        ForEach(0 ..< tipPercentages.count) {
                            Text("\(tipPercentages[$0])%")
                        }
                    }.pickerStyle(SegmentedPickerStyle()) // This wont take user to different page
                }
                // This is the title for number of people within the users group in order the for the app to split the cheque between the group
                Section(header: Text("How many people?")) {
                    // The picker will allow the user to choose how many people are within the grour from 0 - 25 people within the group
                    // $people is the binding string which binds the element of people with the @state above within the logic
                    Picker("Number of people", selection: $people) {
                        // You as the dev can decide any number for the amount of people within the group
                        ForEach(0 ..< 50) {
                            Text("\($0) people")
                        }
                    }
                }
                // This is the title for thee amount each person will have to pay within the group of friends or enemies
                Section(header: Text("Total per person")) {
                    // The currency used is the R = Rand which the South African currency
                    // The dev can input any currency he/she wants to use for this app
                    // The specifier %.2f means that the app will calculate the total price for the 2 decimal places of the price for each member of the group
                    Text("R \(calculateTotal(), specifier: "%.2f")")
                    
                }
                
            }.navigationTitle("Split the Cheque") // this will the title of the app once user opens the app
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```
The image of the app on iPhone 14 pro max:
![Home](https://user-images.githubusercontent.com/87414441/200576765-3246c3dd-d24c-452d-973c-467a98f2f716.png)

![User Interface](https://user-images.githubusercontent.com/87414441/200577346-87525f0a-0b4a-4275-a882-38758d933183.png <)



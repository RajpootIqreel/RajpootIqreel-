import React, { useState } from "react";
import {
  StyleSheet,
  Text,
  View,
  TextInput,
  Button,
  Picker,
} from "react-native";

export default function App() {
  const [billAmount, setBillAmount] = useState("");
  const [tipPercentage, setTipPercentage] = useState("10"); // default tip percentage
  const [numPeople, setNumPeople] = useState("1"); // default to 1 person
  const [totalAmount, setTotalAmount] = useState(null);
  const [amountPerPerson, setAmountPerPerson] = useState(null);

  const calculateTip = () => {
    const bill = parseFloat(billAmount);
    const tipPercent = parseFloat(tipPercentage);
    const people = parseInt(numPeople);

    if (isNaN(bill) || bill <= 0 || isNaN(people) || people <= 0) {
      alert("Please enter valid inputs for bill and number of people");
      return;
    }

    // Calculate the tip and total amount
    const tipAmount = (bill * tipPercent) / 100;
    const total = bill + tipAmount;
    const perPerson = total / people;

    // Update the state to show results
    setTotalAmount(total.toFixed(2));
    setAmountPerPerson(perPerson.toFixed(2));
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Tip Calculator</Text>

      <TextInput
        style={styles.input}
        keyboardType="numeric"
        placeholder="Enter bill amount"
        value={billAmount}
        onChangeText={(value) => setBillAmount(value)}
      />

      <Text style={styles.label}>Tip Percentage</Text>
      <Picker
        selectedValue={tipPercentage}
        style={styles.picker}
        onValueChange={(itemValue) => setTipPercentage(itemValue)}
      >
        <Picker.Item label="10%" value="10" />
        <Picker.Item label="15%" value="15" />
        <Picker.Item label="20%" value="20" />
        <Picker.Item label="Custom" value="custom" />
      </Picker>

      {tipPercentage === "custom" && (
        <TextInput
          style={styles.input}
          keyboardType="numeric"
          placeholder="Enter custom tip percentage"
          value={tipPercentage}
          onChangeText={(value) => setTipPercentage(value)}
        />
      )}

      <TextInput
        style={styles.input}
        keyboardType="numeric"
        placeholder="Number of people"
        value={numPeople}
        onChangeText={(value) => setNumPeople(value)}
      />

      <Button title="Calculate" onPress={calculateTip} />

      {totalAmount && (
        <View style={styles.resultContainer}>
          <Text style={styles.resultText}>Total Amount: ${totalAmount}</Text>
          <Text style={styles.resultText}>
            Each Person Pays: ${amountPerPerson}
          </Text>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: "bold",
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: "gray",
    borderWidth: 1,
    marginBottom: 15,
    width: "100%",
    paddingLeft: 10,
  },
  label: {
    fontSize: 18,
    marginBottom: 10,
  },
  picker: {
    height: 50,
    width: "100%",
    marginBottom: 20,
  },
  resultContainer: {
    marginTop: 20,
    alignItems: "center",
  },
  resultText: {
    fontSize: 18,
    fontWeight: "bold",
    marginVertical: 5,
  },
});

# RajpootIqreel-

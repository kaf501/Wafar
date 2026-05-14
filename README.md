# Wafar
وفر - تطبيق توصيل وكاش باك بالكويت يمنح المستخدم كاش باك على كل طلب.

import React, { useState } from 'react';
import {
  View,
  Text,
  TouchableOpacity,
  StyleSheet,
  ScrollView,
  Alert,
} from 'react-native';

export default function App() {
  const [balance, setBalance] = useState(0);

  const restaurants = [
    { name: 'قهوة وفر', price: 5 },
    { name: 'برغر وفر', price: 7 },
    { name: 'بيتزا وفر', price: 6 },
  ];

  const orderNow = (price) => {
    const cashback = price * 0.03;
    const newBalance = balance + cashback;

    setBalance(newBalance);

    Alert.alert(
      'تم الطلب 🎉',
      `تم إضافة ${cashback.toFixed(3)} د.ك كاش باك إلى محفظتك`
    );
  };

  return (
    <ScrollView style={styles.container}>
      <Text style={styles.logo}>وفر</Text>

      <View style={styles.wallet}>
        <Text style={styles.walletTitle}>رصيد الكاش باك</Text>
        <Text style={styles.walletAmount}>
          {balance.toFixed(3)} د.ك
        </Text>
      </View>

      <Text style={styles.section}>المطاعم والقهاوي</Text>

      {restaurants.map((item, index) => (
        <View key={index} style={styles.card}>
          <View>
            <Text style={styles.restaurant}>{item.name}</Text>
            <Text style={styles.price}>
              قيمة الطلب: {item.price} د.ك
            </Text>
            <Text style={styles.cashback}>
              كاش باك 3%
            </Text>
          </View>

          <TouchableOpacity
            style={styles.button}
            onPress={() => orderNow(item.price)}
          >
            <Text style={styles.buttonText}>اطلب الآن</Text>
          </TouchableOpacity>
        </View>
      ))}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5F3FF',
    padding: 20,
  },
  logo: {
    fontSize: 42,
    fontWeight: 'bold',
    color: '#6D28D9',
    textAlign: 'center',
    marginTop: 50,
    marginBottom: 30,
  },
  wallet: {
    backgroundColor: '#6D28D9',
    borderRadius: 22,
    padding: 25,
    marginBottom: 30,
  },
  walletTitle: {
    color: 'white',
    fontSize: 18,
  },
  walletAmount: {
    color: 'white',
    fontSize: 34,
    fontWeight: 'bold',
    marginTop: 10,
  },
  section: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 15,
    color: '#111827',
  },
  card: {
    backgroundColor: 'white',
    borderRadius: 18,
    padding: 20,
    marginBottom: 15,
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
  },
  restaurant: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#111827',
  },
  price: {
    marginTop: 6,
    color: '#374151',
  },
  cashback: {
    marginTop: 6,
    color: '#6D28D9',
    fontWeight: 'bold',
  },
  button: {
    backgroundColor: '#6D28D9',
    paddingHorizontal: 18,
    paddingVertical: 12,
    borderRadius: 14,
  },
  buttonText: {
    color: 'white',
    fontWeight: 'bold',
  },
});

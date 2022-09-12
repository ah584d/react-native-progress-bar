# react-native-progress-bar
animated progress bar

```
import React, { ReactElement, useEffect } from 'react';
import Animated, { interpolate, useAnimatedStyle, useSharedValue, withTiming } from 'react-native-reanimated';
import { StyleSheet, View } from 'react-native';
import { horizontalScale } from '@common/constants';

interface Props {
  stepPercentage: number;
}

const PROGRESS_BAR_MAX_VALUE = horizontalScale(167);

export const ProgressBar = ({ stepPercentage }: Props): ReactElement => {
  const barWidthAnimation = useSharedValue(25); // stands for 25%

  const progressPercent = useAnimatedStyle(() => {
    const width = interpolate(barWidthAnimation.value, [0, 100], [0, PROGRESS_BAR_MAX_VALUE]);
    return {
      width,
    };
  });

  useEffect(() => {
    if (isNaN(stepPercentage)) {
      return;
    }
    barWidthAnimation.value = withTiming(stepPercentage, { duration: 500 });
  }, [stepPercentage]);

  return (
    <View style={styles.layout}>
      <Animated.View style={[styles.bar, progressPercent]} />
    </View>
  );
};

const styles = StyleSheet.create({
  layout: {
    backgroundColor: #, // add color from props
    color: theme.colors.activeIndicator,
    height: 4,
    borderRadius: 20,
    width: horizontalScale(167),
  },
  bar: {
    backgroundColor: #,// add color from props
    height: 4,
    borderRadius: 20,
  },
});
```

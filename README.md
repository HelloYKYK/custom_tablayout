# 可以自定义indicator宽度（自定义tabLayout指示器宽度）的tabLayout
* 复制了tablayout的源码进行了修改
* 默认宽度为等于tab的文字宽度
* 通过tabLayout.setIndicatorWidth(int dp)自定义indicator的宽度

> 缺点是，indicator的动画变得不自然了
```java
private void updateIndicatorPosition() {
            final View selectedTitle = getChildAt(mSelectedPosition);
            int left, right;
            if (selectedTitle != null && selectedTitle.getWidth() > 0) {
                left = selectedTitle.getLeft();
                right = selectedTitle.getRight();
                // TODO: 16/9/21 调试if
                if (selectedTitle instanceof TabView){
//                    TextPaint paint = ((TextView) selectedTitle).getPaint();
//                    //文字左右平分距left和right的宽度
                    float textPaintWidth = indecatorWidth==0? ((TabView) selectedTitle).getTabTextWidth():
                            indecatorWidth;
                    ((TabView) selectedTitle).getTabTextWidth();
                    float newLeft = (right-left-textPaintWidth)/2;
                    left = (int) (left+newLeft);
                    right = (int) (left+textPaintWidth);
                }
                if (mSelectionOffset > 0f && mSelectedPosition < getChildCount() - 1) {
                    // Draw the selection partway between the tabs
                    View nextTitle = getChildAt(mSelectedPosition + 1);
                    View nowTitle = getChildAt(mSelectedPosition);
                    left = (int) (mSelectionOffset * nextTitle.getLeft() +
                            (1.0f - mSelectionOffset) * left);
                    right = (int) (mSelectionOffset * nextTitle.getRight() +
                            (1.0f - mSelectionOffset) * right);
                }
            } else {
                left = right = -1;
            }

            setIndicatorPosition(left, right);
        }
```
* 加入了自定义indicator宽度的方法：
```java
    public void  setIndicatorWidth(int dp) {
        this.indecatorWidth =  DpAndPx.convertDpToPixel(dp);
    }
```

---
title: "LayoutGroup"
excerpt: 'Arranges child nodes in a horizontal row or vertical column with configurable spacing and alignment'
deprecated: false
hidden: false
metadata:
  title: 'LayoutGroup'
  description: 'The LayoutGroup node arranges child nodes in a horizontal row or vertical column, with fields to control item spacing, horizontal and vertical alignment, and margins around the edges of the group.'
  robots: index
next:
  description: ''
---
Extends [**Group**](doc:group)

The LayoutGroup node class manages the position of its child nodes by arranging them in a row from left to right (horizontal layout), or in a column from top to bottom (vertical layout). Fields provide options to control the spacing between children, the horizontal and vertical alignment, and the margins around the edges of the group.

## Fields

<table>
  <thead>
    <tr>
      <th class="short-line" style={{ textAlign: "left" }}>Field</th>
      <th class="short-line" style={{ textAlign: "left" }}>Type</th>
      <th class="short-line" style={{ textAlign: "left" }}>Default</th>
      <th class="short-line" style={{ textAlign: "left" }}>Access Permission</th>
      <th class="long-line" style={{ textAlign: "left" }}>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="short-line">layoutDirection</td>
      <td class="short-line">string</td>
      <td class="short-line">vert</td>
      <td class="short-line">READ_WRITE</td>
      <td class="long-line">
        Controls the layout direction.
        <div class="hscroll">
        <table>
          <thead>
            <tr><th class="short-line" style={{ textAlign: "left" }}>Value</th><th class="short-line" style={{ textAlign: "left" }}>Use</th></tr>
          </thead>
          <tbody>
            <tr><td class="short-line">horiz</td><td class="long-line">Positions the children in a row from left to right</td></tr>
            <tr><td class="short-line">vert</td><td class="long-line">Positions the children in a column from top to bottom</td></tr>
          </tbody>
        </table>
        </div>
      </td>
    </tr>
    <tr>
      <td class="short-line">horizAlignment</td>
      <td class="short-line">string</td>
      <td class="short-line">left</td>
      <td class="short-line">READ_WRITE</td>
      <td class="long-line">
        Specifies the alignment point in the horizontal direction. The effect of the value set depends on whether the layoutDirection field value is set to horiz or vert.
        <div class="hscroll">
        <table>
          <thead>
            <tr><th class="short-line" style={{ textAlign: "left" }}>Value</th><th class="short-line" style={{ textAlign: "left" }}>layoutDirection</th><th class="short-line" style={{ textAlign: "left" }}>Use</th></tr>
          </thead>
          <tbody>
            <tr><td class="short-line">left</td><td class="short-line">vert</td><td class="long-line">Aligns the left edges of each child in the column, and sets the LayoutGroup node local x-coordinate origin at the left edge of the children</td></tr>
            <tr><td class="short-line">left</td><td class="short-line">horiz</td><td class="long-line">Sets the LayoutGroup node local x-coordinate origin at the left edge of the first child</td></tr>
            <tr><td class="short-line">center</td><td class="short-line">vert</td><td class="long-line">Aligns the centers of each child in the column, and sets the LayoutGroup node local x-coordinate origin at the center alignment point</td></tr>
            <tr><td class="short-line">center</td><td class="short-line">horiz</td><td class="long-line">Sets the LayoutGroup node local x-coordinate origin at the center of the horizontal row of children</td></tr>
            <tr><td class="short-line">right</td><td class="short-line">vert</td><td class="long-line">Aligns the right edges of each child in the column, and sets the <strong>LayoutGroup</strong> node local x-coordinate origin at the right edge of the children</td></tr>
            <tr><td class="short-line">right</td><td class="short-line">horiz</td><td class="long-line">Sets the LayoutGroup node local x-coordinate origin at the right edge of the last child</td></tr>
            <tr><td class="short-line">custom</td><td class="short-line">vert</td><td class="long-line">Explicitly set the x translation of each child of the LayoutGroup. If the layoutDirection is "horiz", custom is not a valid setting; "left" is used instead.</td></tr>
          </tbody>
        </table>
        </div>
      </td>
    </tr>
    <tr>
      <td class="short-line">vertAlignment</td>
      <td class="short-line">string</td>
      <td class="short-line">top</td>
      <td class="short-line">READ_WRITE</td>
      <td class="long-line">
        Specifies the alignment point in the vertical direction. The effect of the value set depends on whether the layoutDirection field value is set to horiz or vert.
        <div class="hscroll">
        <table>
          <thead>
            <tr><th class="short-line" style={{ textAlign: "left" }}>Value</th><th class="short-line" style={{ textAlign: "left" }}>layoutDirection</th><th class="short-line" style={{ textAlign: "left" }}>Use</th></tr>
          </thead>
          <tbody>
            <tr><td class="short-line">top</td><td class="short-line">horiz</td><td class="long-line">Aligns the top edges of each child in the row, and sets the <strong>LayoutGroup</strong> node local y-coordinate origin at the top edge of the children</td></tr>
            <tr><td class="short-line">top</td><td class="short-line">vert</td><td class="long-line">Sets the LayoutGroup node local y-coordinate origin at the top edge of the first child</td></tr>
            <tr><td class="short-line">center</td><td class="short-line">horiz</td><td class="long-line">Aligns the centers of each child in the row, and sets the LayoutGroup node local y-coordinate origin at the center alignment point</td></tr>
            <tr><td class="short-line">center</td><td class="short-line">vert</td><td class="long-line">Sets the <strong>LayoutGroup</strong> node local y-coordinate origin at the center of the vertical column of children</td></tr>
            <tr><td class="short-line">bottom</td><td class="short-line">horiz</td><td class="long-line">Aligns the bottom edges of each child in the row, and sets the <strong>LayoutGroup</strong> node local y-coordinate origin at the bottom edge of the children</td></tr>
            <tr><td class="short-line">bottom</td><td class="short-line">vert</td><td class="long-line">Sets the LayoutGroup node local y-coordinate origin at the bottom edge of the last child</td></tr>
            <tr><td class="short-line">custom</td><td class="short-line">horiz</td><td class="long-line">Explicitly set the y translation of each child of the LayoutGroup. If the layoutDirection is "vert", custom is not a valid setting; "top" is used instead.</td></tr>
          </tbody>
        </table>
        </div>
      </td>
    </tr>
    <tr>
      <td class="short-line">itemSpacings</td>
      <td class="short-line">array of floats</td>
      <td class="short-line">[ ]</td>
      <td class="short-line">READ_WRITE</td>
      <td class="long-line">Controls the spacing before or after each child in the layout direction. By default, no space is added between the children.</td>
    </tr>
    <tr>
      <td class="short-line">addItemSpacingAfterChild</td>
      <td class="short-line">Boolean</td>
      <td class="short-line">true</td>
      <td class="short-line">READ_WRITE</td>
      <td class="long-line">Controls how the spaces specified in the itemSpacings field are inserted. By default, the field value is set to true. This causes the specified spaces to be inserted after the child is positioned. If the field value is set to false, the specified item space is inserted before the child is positioned.</td>
    </tr>
  </tbody>
</table>

NewQuickAction3D
================

NewQuickAction3D is a small android library to create QuickAction dialog with Gallery3D app style.

How to Use
==========
This repo includes a sample Activity (__ExampleActivity.java__) to show how to use QuickAction.

	public class ExampleActivity extends Activity {
	//action id
	private static final int ID_UP     = 1;
	private static final int ID_DOWN   = 2;
	private static final int ID_SEARCH = 3;
	private static final int ID_INFO   = 4;
	private static final int ID_ERASE  = 5;	
	private static final int ID_OK     = 6;
	    
	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);

		setContentView(R.layout.main);

		ActionItem nextItem 	= new ActionItem(ID_DOWN, "Next", getResources().getDrawable(R.drawable.menu_down_arrow));
		ActionItem prevItem 	= new ActionItem(ID_UP, "Prev", getResources().getDrawable(R.drawable.menu_up_arrow));
        ActionItem searchItem 	= new ActionItem(ID_SEARCH, "Find", getResources().getDrawable(R.drawable.menu_search));
        ActionItem infoItem 	= new ActionItem(ID_INFO, "Info", getResources().getDrawable(R.drawable.menu_info));
        ActionItem eraseItem 	= new ActionItem(ID_ERASE, "Clear", getResources().getDrawable(R.drawable.menu_eraser));
        ActionItem okItem 		= new ActionItem(ID_OK, "OK", getResources().getDrawable(R.drawable.menu_ok));
        
        //use setSticky(true) to disable QuickAction dialog being dismissed after an item is clicked
        prevItem.setSticky(true);
        nextItem.setSticky(true);
		
		//create QuickAction. Use QuickAction.VERTICAL or QuickAction.HORIZONTAL param to define layout 
        //orientation
        
		final QuickAction quickVerticalAction = new QuickAction(this, QuickAction.VERTICAL);
		final QuickAction quickHorizontalAction = new QuickAction(this, QuickAction.HORIZONTAL);
		
		//add action items into QuickAction
		quickVerticalAction.addActionItem(nextItem);
        quickVerticalAction.addActionItem(prevItem);
        quickVerticalAction.addActionItem(searchItem);
        quickVerticalAction.addActionItem(infoItem);
        quickVerticalAction.addActionItem(eraseItem);
        quickVerticalAction.addActionItem(okItem);
        
        quickHorizontalAction.addActionItem(nextItem);
        quickHorizontalAction.addActionItem(prevItem);
        quickHorizontalAction.addActionItem(searchItem);
        quickHorizontalAction.addActionItem(infoItem);
        quickHorizontalAction.addActionItem(eraseItem);
        quickHorizontalAction.addActionItem(okItem);

        //Set listener for action item clicked
        quickVerticalAction.setOnActionItemClickListener(new QuickAction.OnActionItemClickListener() {			
			@Override
			public void onItemClick(QuickAction source, int pos, int actionId) {				
				ActionItem actionItem = quickVerticalAction.getActionItem(pos);
                 
				//here we can filter which action item was clicked with pos or actionId parameter
				if (actionId == ID_SEARCH) {
					Toast.makeText(getApplicationContext(), "Let's do some search action", Toast.LENGTH_SHORT).show();
				} else if (actionId == ID_INFO) {
					Toast.makeText(getApplicationContext(), "I have no info this time", Toast.LENGTH_SHORT).show();
				} else {
					String tag = (String) source.getLastAnchorView().getTag();
					if(tag==null){
						Toast.makeText(getApplicationContext(), actionItem.getTitle() + " selected", Toast.LENGTH_SHORT).show();
					} else {
						Toast.makeText(getApplicationContext(), actionItem.getTitle() + " selected and view's Tag is '" + tag + "'", Toast.LENGTH_SHORT).show();
					}
				}
			}
		});
		
        
        quickHorizontalAction.setOnActionItemClickListener(new QuickAction.OnActionItemClickListener() {			
			@Override
			public void onItemClick(QuickAction source, int pos, int actionId) {				
				ActionItem actionItem = quickVerticalAction.getActionItem(pos);
                 
				//here we can filter which action item was clicked with pos or actionId parameter
				if (actionId == ID_SEARCH) {
					Toast.makeText(getApplicationContext(), "Let's do some search action", Toast.LENGTH_SHORT).show();
				} else if (actionId == ID_INFO) {
					Toast.makeText(getApplicationContext(), "I have no info this time", Toast.LENGTH_SHORT).show();
				} else {
					String tag = (String) source.getLastAnchorView().getTag();
					if(tag==null){
						Toast.makeText(getApplicationContext(), actionItem.getTitle() + " selected", Toast.LENGTH_SHORT).show();
					} else {
						Toast.makeText(getApplicationContext(), actionItem.getTitle() + " selected and view's Tag is '" + tag + "'", Toast.LENGTH_SHORT).show();
					}
				}
			}
		});
        
		//set listnener for on dismiss event, this listener will be called only if QuickAction dialog was dismissed
		//by clicking the area outside the dialog.
        quickVerticalAction.setOnDismissListener(new QuickAction.OnDismissListener() {			
			@Override
			public void onDismiss() {
				Toast.makeText(getApplicationContext(), "Dismissed", Toast.LENGTH_SHORT).show();
			}
		});
		
		//show on btn1
		Button btn1 = (Button) this.findViewById(R.id.btn1);
		btn1.setOnClickListener(new View.OnClickListener() {
			@Override
			public void onClick(View v) {
				quickVerticalAction.show(v);
			}
		});

		Button btn2 = (Button) this.findViewById(R.id.btn2);
		btn2.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View v) {
				quickVerticalAction.show(v);
			}
		});
		
		Button btn3 = (Button) this.findViewById(R.id.btn3);
		btn3.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View v) {
				quickVerticalAction.show(v);
				quickVerticalAction.setAnimStyle(QuickAction.ANIM_REFLECT);
			}
		});
		
		Button btn4 = (Button) this.findViewById(R.id.btn4);
		btn4.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View v) {
				quickVerticalAction.show(v);
				quickVerticalAction.setAnimStyle(QuickAction.ANIM_REFLECT);
			}
		});
		
		Button btn5 = (Button) this.findViewById(R.id.btn5);
		btn5.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View v) {
				quickHorizontalAction.show(v);
			}
		});
		
		Button btn6 = (Button) this.findViewById(R.id.btn6);
		btn6.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View v) {
				quickHorizontalAction.show(v, getResources().getDrawable(R.drawable.icon), "Line1", "Line2");
			}
		});
	}
  }

**See http://www.londatiga.net/it/how-to-create-quickaction-dialog-in-android/ for more information.**

![Example Image](http://londatiga.net/images/quickaction3d_horizontal.png)  ![Example Image](http://londatiga.net/images/quickaction3d_vertical.png) 
![Example Image](http://aschillings.co.uk/assets/images/android_quickactions3d_with_icon.png)  ![Example Image](http://aschillings.co.uk/assets/images/android_quickactions3d.png) 

Developed By
============

* Lorensius W. L. T - <lorenz@londatiga.net>

Contributors
============

* Kevin Peck - <kevinwpeck@gmail.com>
* [Alexandros Schillings](https://github.com/alt236)

Changes
=======

See [CHANGELOG](https://github.com/lorensiuswlt/NewQuickAction3D/blob/master/CHANGELOG.md) for details

License
=======

    Copyright 2011 Lorensius W. L. T

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
# Adding-money-to-the-pile
How adding the betting money and checking your hand works in Java fx
4/3/2020

With this program, you will be able to see how much money you win or lose from your hand choice.

To install the code you would need to make sure you have all the downloads for Javafx and use JDK8.

  As the code compiles, it will start to add the money of your standard 200. you will change the text of the 200 when the hand is a win hand. And you may still gain only 4 cards and i still have not fixed the issue, maybe you may find a soulltion for this issue. But as the prgram goes down it evaluates the cards you have and if your hand is the highest hand value thne you would change the value 
of the money the player earned which is double.

//******************************************************************
// COSC 1174.48L
// Bralon Holmes
// April 4, 2020
// Adding a bet amount and checking the hand
//******************************************************************
package WindowTest;
import java.util.Scanner;
import java.io.File;
import java.util.ArrayList;
import javafx.scene.control.RadioButton;
import javafx.scene.control.ToggleGroup;
import javafx.animation.Interpolator;
import javafx.animation.PathTransition;
import javafx.animation.RotateTransition;
import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Node;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.scene.shape.LineTo;
import javafx.scene.shape.MoveTo;
import javafx.scene.shape.Path;
import javafx.scene.transform.Rotate;
import javafx.stage.Stage;
import javafx.util.Duration;
import javafx.scene.control.Label;
public class Poker1 extends Application {
	
	boolean hold1 = false;
	boolean hold2 = false;
	boolean hold3 = false;
	boolean hold4 = false;
	boolean hold5 = false;
	
			ArrayList<Integer> cards = new ArrayList<Integer>();
	ArrayList<ImageView> images = new ArrayList<ImageView>();
	
	
	private static int Money = 200;
			private static int $200;
 
	//Creates an array of 52 cards
	@Override // override the start of the application
	public void start(Stage primaryStage) {
		
		for (int i = 0; i < 52; i++) {
			cards.add(i);
		}
		for(int i = 0; i < 5; i++)
			images.add(new ImageView());
		
		// Create a VBox
		VBox vBox = new VBox(10);
		vBox.setPadding(new Insets(10, 10, 10, 10));

		// Creates pane to hold the cards
		HBox hBox = new HBox(10);
		hBox.setPadding(new Insets(10, 10, 10, 40));
		hBox.getChildren().addAll(images);
		draw(hBox);

		HBox holdBox = new HBox(10);
		holdBox.setPadding(new Insets(10, 10, 10, 10));

		Button btDEAL = new Button("DEAL");
		btDEAL.setOnAction(e -> draw(hBox));
		
		Button btdraw = new Button("DRAW");
		btdraw.setOnAction(e -> draw(hBox));
		
		//Creates hold button to hold cards
		Button bthold1 = new Button("HOLD");
		bthold1.setOnAction(new Hold1Handler());
		Button bthold2 = new Button("HOLD");
		bthold2.setOnAction(new Hold2Handler());
		Button bthold3 = new Button("HOLD");
		bthold3.setOnAction(new Hold3Handler());
		Button bthold4 = new Button("HOLD");
		bthold4.setOnAction(new Hold4Handler());
		Button bthold5 = new Button("HOLD");
		bthold5.setOnAction(new Hold5Handler());
		
		Label welcome = new Label("$400");
		
		RadioButton r1 = new RadioButton("$1");
		RadioButton r2 = new RadioButton("$10");
		RadioButton r3 = new RadioButton("$100");
		
		ToggleGroup tg = new ToggleGroup();
		r1.setToggleGroup(tg);
		r2.setToggleGroup(tg);
		r3.setToggleGroup(tg);
		
		
		holdBox.getChildren().addAll(bthold1, bthold2, bthold3, bthold4, bthold5);

		
		vBox.getChildren().addAll(hBox, holdBox, btdraw, btDEAL, r1, r2, r3, welcome);
		
if (r1.isSelected()) {
			Money = Money - 1;
			}
			if (r2.isSelected()) {
			Money = Money - 10;
			} 
			if (r3.isSelected()) {
			Money = Money - 100;
			}
		
			// Creates the window with the pane inside
		Scene scene = new Scene(vBox, 500, 500);
		primaryStage.setTitle("Poker Five Cards");
		primaryStage.setScene(scene);
		primaryStage.show();
	
		
	}

	
	public static void main(String args[]) {
		launch(args);
	}

	

	public void draw(HBox pane) {
		// shuffle deck
		java.util.Collections.shuffle(cards);

		// The card will be swaped if not under the hold button
		if (hold1 == false) {
			exit(images.get(0), 1);
			new java.util.Timer().schedule(
			new java.util.TimerTask() {
			@Override
			public void run() {
			Image image1 = new Image(new File("card\\" + cards.get(0) + ".png").toURI().toString());
			images.get(0).setImage(image1);
			enter(images.get(0), 1);
						}
					},
					1000
			);
		}
		else {
			new PathTransition(Duration.ZERO, new Path(new MoveTo(0,50)), images.get(0)).play();
		}
		//If card not under hold then the card will flip and a new image shows up
		if (hold2 == false) {
			exit(images.get(1), 2);
			new java.util.Timer().schedule(
			new java.util.TimerTask() {
			@Override
			public void run() {
			Image image2 = new Image(new File("card\\" + cards.get(1) + ".png").toURI().toString());
			images.get(1).setImage(image2);
			enter(images.get(1), 2);
						}
					},
					1000
			);
		}
		else {
			new PathTransition(Duration.ZERO, new Path(new MoveTo(0,50)), images.get(1)).play();
		}
		
		if (hold3 == false) {
			exit(images.get(2), 3);
			new java.util.Timer().schedule(
			new java.util.TimerTask() {
			@Override
			public void run() {
			Image image3 = new Image(new File("card\\" + cards.get(2) + ".png").toURI().toString());
			images.get(2).setImage(image3);
			enter(images.get(2), 3);
						}
					},
					1000
			);
		}
		else {
			new PathTransition(Duration.ZERO, new Path(new MoveTo(0,50)), images.get(2)).play();
		}
		
		if (hold4 == false) {
			exit(images.get(3), 4);
			new java.util.Timer().schedule(
			new java.util.TimerTask() {
			@Override
			public void run() {
			Image image4 = new Image(new File("card\\" + cards.get(3) + ".png").toURI().toString());
			images.get(3).setImage(image4);
			enter(images.get(3), 4);
						}
					},
					1000
			);
		}
		else {
			new PathTransition(Duration.ZERO, new Path(new MoveTo(0,50)), images.get(4)).play();
		}
		
		if (hold5 == false) {
			exit(images.get(4), 5);
			new java.util.Timer().schedule(
			new java.util.TimerTask() {
			@Override
			public void run() {
			Image image5 = new Image(new File("card\\" + cards.get(4) + ".png").toURI().toString());
			images.get(4).setImage(image5);
			enter(images.get(4), 5);
						}
					},
					1000
			);
		}
		else {
			new PathTransition(Duration.ZERO, new Path(new MoveTo(0,50)), images.get(4)).play();
		}
		
		
	}
	private void enter(Node card, int pos) 
	{
		//A timer is set the card to flip
		PathTransition path = new PathTransition();
		path.setDuration(Duration.millis(1000));
		path.setNode(card);
		path.setPath(new Path(new MoveTo(0, -300), new LineTo(0, 50)));
		path.play();
	}
	
		private void exit(Node card, int pos) 
		{
			((ImageView)card).setImage(new Image(new File("card\\b2fv.png").toURI().toString()));
		PathTransition path = new PathTransition();
		path.setDuration(Duration.millis(1000));
		path.setNode(card);
		path.setPath(new Path(new MoveTo(0,50), new LineTo(0,600)));
		path.play();
	}
	public static int get$200() {
			return $200;
		}


		public static void set$200(int $200) {
			Poker1.$200 = $200;
		}
	//if the card is under the hold button it is true, if not it is false
	class Hold1Handler implements EventHandler<ActionEvent> {
		@Override
		public void handle(ActionEvent e) {
			if (hold1 == true) {
				hold1 = false;
			} else if (hold1 == false) {
				hold1 = true;
			}
		}
	}

	class Hold2Handler implements EventHandler<ActionEvent> {
		@Override
		public void handle(ActionEvent e) {
			if (hold2 == true) {
				hold2 = false;
			} else if (hold2 == false) {
				hold2 = true;
			}
		}
	}

	class Hold3Handler implements EventHandler<ActionEvent> {
		@Override
		public void handle(ActionEvent e) {
			if (hold3 == true) {
				hold3 = false;
			} else if (hold3 == false) {
				hold3 = true;
			}
		}
	}

	class Hold4Handler implements EventHandler<ActionEvent> {
		@Override
		public void handle(ActionEvent e) {
			if (hold4 == true) {
				hold4 = false;
			} else if (hold4 == false) {
				hold4 = true;
			}
		}
	}

	class Hold5Handler implements EventHandler<ActionEvent> {
		@Override
		public void handle(ActionEvent e) {
			if (hold5 == true) {
				hold5 = false;
			} else if (hold5 == false) {
				hold5 = true;
			}
		}
	}


//evaluates the hand

	public void evaluate()

	{

		if (this.royalFlush() == 1)

		{

			System.out.println("You have a royal flush!");

		}

		else if (this.straightFlush() == 1)

		{

			System.out.println("You have a straight flush!");

		}

		else if (this.fourOfaKind() == 1)

		{

			System.out.println("You have four of a kind!");

		}

		else if (this.fullHouse() == 1)

		{

			System.out.println("You have a full house!");

		}

		else if (this.flush() == 1)

		{

			System.out.println("You have a flush!");

		}

		else if (this.straight() == 1)

		{

			System.out.println("You have a straight!");

		}

		else if (this.triple() == 1)

		{

			System.out.println("You have a triple!");

		}

		else if (this.twoPairs() == 1)

		{

			System.out.println("You have two pairs!");

		}

		else if (this.pair() == 1)

		{

			System.out.println("You have a pair!");

		}

		else

		{

		}

	}

	

	// checks for a royal flush

	public int royalFlush()

	{

		if (cards.get(0) == 1 && cards.get(1) == 10 && cards.get(2) == 11 &&

				cards.get(3) == 12 && cards.get(4) == 13)

		{

			return 1;

		}

		else

		{

			return 0;

		}

	}

	

	// checks for a straight flush

	public int straightFlush()

	{

		for (int counter = 1; counter < 5; counter++)

		{

			if (cards.get(0) != cards.get(counter))

			{

				return 0;

			}

		}

		for (int counter2 = 1; counter2 < 5; counter2++)

		{

			if (cards.get(counter2 - 1) != (cards.get(counter2) - 1))

			{

				return 0;

			}

				

		}

		return 1;

		

	}

	

	// checks for four of a kind

	public int fourOfaKind()

	{

		if (cards.get(0) != cards.get(3) && cards.get(1) != cards.get(4))

		{

			return 0;

		}

		else

		{

			return 1;

		}

	}

	

	// checks for full house

	public int fullHouse()

	{

		int comparison = 0;

		for (int counter = 1; counter < 5; counter++)

		{

			if (cards.get(counter - 1) == cards.get(counter))

			{

				comparison++;

			}

		}

		if (comparison == 3)

		{

			return 1;

		}

		else

		{

			return 0;

		}

	}

	

	// checks for flush

	public int flush()

	{

		for (int counter = 1; counter < 5; counter++)

		{

			if (cards.get(0) != cards.get(counter))

			{

				return 0;

			}

		}

		return 1;

	}

	

	// check for straight

	public int straight()

	{

		for (int counter2 = 1; counter2 < 5; counter2++)

		{

			if (cards.get(counter2 - 1) != (cards.get(counter2) - 1))

			{

				return 0;

			}

				

		}

		return 1;

	}

	

	// checks for triple

	public int triple()

	{

		if (cards.get(0) == cards.get(2) || cards.get(2) == cards.get(4))

		{

			return 1;

		}

		return 0;

	}

	

	// checks for two pairs

	public int twoPairs()

	{

		int check = 0;

		for(int counter = 1; counter < 5; counter++)

		{

			if (cards.get(counter - 1) == cards.get(counter))

			{

				check++;

			}

		}

		if (check == 2)

		{

			return 1;

		}

		else

		{

			return 0;

		}

	}

	

	// check for pair

	public int pair()

	{

		int check = 0;

		for(int counter = 1; counter < 5; counter++)

		{

			if (cards.get(counter - 1) == cards.get(counter))

			{

				check++;

			}

		}

		if (check == 1)

		{

			return 1;

		}

		else

		{

			return 0;

		}

	}
}

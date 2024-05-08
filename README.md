package application;
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.input.KeyCode;
import javafx.scene.input.MouseEvent;
import javafx.scene.layout.AnchorPane;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

import java.util.HashMap;
import java.util.Map;

public class Main extends Application {

    private ListView<String> listView;
    private TextField newInfoTextField;
    private Map<String, String> labelData;

    @Override
    public void start(Stage primaryStage) {
        try {
            BorderPane root = new BorderPane();

            // Crear el AnchorPane para las imágenes y etiquetas
            AnchorPane leftPane = new AnchorPane();

            // Cargar las imágenes
            Image image1 = new Image("file:///C:/Users/brayt/eclipse-workspace/taller/clientes/Jose.png");
            Image image2 = new Image("file:///C:/Users/brayt/eclipse-workspace/taller/clientes/Juan.png");
            Image image3 = new Image("file:///C:/Users/brayt/eclipse-workspace/taller/clientes/Maria.png");
            Image image4 = new Image("file:///C:/Users/brayt/eclipse-workspace/taller/clientes/Mark.png");
            // Crear ImageViews y ajustar tamaño
            
            ImageView imageView1 = new ImageView(image1);
            ImageView imageView2 = new ImageView(image2);
            ImageView imageView3 = new ImageView(image3);
            ImageView imageView4 = new ImageView(image4);

            double imageWidth = 80;
            double imageHeight = 80;

            imageView1.setFitWidth(imageWidth);
            imageView1.setFitHeight(imageHeight);
            imageView2.setFitWidth(imageWidth);
            imageView2.setFitHeight(imageHeight);
            imageView3.setFitWidth(imageWidth);
            imageView3.setFitHeight(imageHeight);
            imageView4.setFitWidth(imageWidth);
            imageView4.setFitHeight(imageHeight);


            // Crear etiquetas para las imágenes
            Label label1 = new Label("Jose", imageView1);
            Label label2 = new Label("Juan " ,imageView2);
            Label label3 = new Label("Maria ", imageView3);
            Label label4 = new Label("Mark", imageView4);

            // Datos almacenados para cada etiqueta
            labelData = new HashMap<>();
            labelData.put("Etiqueta 1", "Cedula: 0909191919, Edad: 22, Pais: Ecuador");
            labelData.put("Etiqueta 2", "Cedula: 0355151515, Edad: 26, Pais: Ecuador");
            labelData.put("Etiqueta 3", "Cedula: 0505055050, Edad: 28, Pais: Ecuador");
            labelData.put("Etiqueta 4", "Cedula: 0954572727, Edad: 20, Pais: Ecuador");
            
            // Manejo de eventos para clics en las etiquetas
            label1.addEventHandler(MouseEvent.MOUSE_CLICKED, e -> listView.getItems().add(labelData.get("Etiqueta 1")));
            label2.addEventHandler(MouseEvent.MOUSE_CLICKED, e -> listView.getItems().add(labelData.get("Etiqueta 2")));
            label3.addEventHandler(MouseEvent.MOUSE_CLICKED, e -> listView.getItems().add(labelData.get("Etiqueta 3")));
            label4.addEventHandler(MouseEvent.MOUSE_CLICKED, e -> listView.getItems().add(labelData.get("Etiqueta 4")));

            // Ubicar elementos en el AnchorPane
            leftPane.getChildren().addAll(label1, label2, label3, label4);

            // Posicionar las etiquetas de forma vertical sin tocarse
            AnchorPane.setTopAnchor(label1, 20.0);
            AnchorPane.setLeftAnchor(label1, 20.0);

            AnchorPane.setTopAnchor(label2, 100.0);
            AnchorPane.setLeftAnchor(label2, 20.0);

            AnchorPane.setTopAnchor(label3, 180.0);
            AnchorPane.setLeftAnchor(label3, 20.0);

            AnchorPane.setTopAnchor(label4, 270.0);
            AnchorPane.setLeftAnchor(label4, 20.0);

            // Configuración de la parte derecha del BorderPane
            AnchorPane rightPane = new AnchorPane();

            listView = new ListView<>();
            rightPane.getChildren().add(listView);
            
            AnchorPane.setTopAnchor(listView, 20.0);
            AnchorPane.setLeftAnchor(listView, 10.0);
            AnchorPane.setRightAnchor(listView, 20.0);
            AnchorPane.setBottomAnchor(listView, 150.0);

            newInfoTextField = new TextField();
            newInfoTextField.setPromptText("Ingresar informacion");
            newInfoTextField.setStyle("-fx-background-color: black ; -fx-text-fill: white;");

         // Para el ListView
            listView.setStyle("-fx-background-color: black; -fx-text-fill: blue;");
            rightPane.getChildren().add(newInfoTextField);

            AnchorPane.setBottomAnchor(newInfoTextField, 50.0);
            AnchorPane.setLeftAnchor(newInfoTextField, 170.0);
            AnchorPane.setRightAnchor(newInfoTextField, 30.0);

            // Guardar información al presionar Enter
            newInfoTextField.setOnKeyPressed(event -> {
                if (event.getCode() == KeyCode.ENTER) {
                    String newText = newInfoTextField.getText();
                    if (!newText.isEmpty()) {
                        listView.getItems().add(newText);
                        newInfoTextField.clear();
                    }
                }
            });

            root.setLeft(leftPane);
            root.setRight(rightPane);

            // Crear la escena y mostrarla
            Scene scene = new Scene(root, 800, 600);
            // Aquí puedes agregar estilos CSS o modificar las propiedades directamente si lo deseas
            // Ejemplo:
            // listView.setStyle("-fx-background-color: lightblue;");
            // newInfoTextField.setStyle("-fx-background-color: lightgray;");
            primaryStage.setTitle("Aplicación con Etiquetas y ListView");
            primaryStage.setScene(scene);
            primaryStage.show();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        launch(args);
    }

}

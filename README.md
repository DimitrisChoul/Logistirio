# Logistirio
import java.util.ArrayList;
import java.util.Scanner;

abstract class CostAccount { //geniki klassi dapani
protected String code;
protected String description;

protected CostAccount() {}

protected CostAccount(String code, String descr) {
	this.code = code;
	this.description = descr;
}

protected void setCode(String code) {this.code = code;}
protected String getCode() {return code;}

protected void setDescription(String descr) {this.description = descr;}
protected String getDescription() {return description;}

protected void calculateCostPerMonth(){}; //mono dilosi oxi ylopoiisi
}

class Fixed extends CostAccount { //klassi pagio
private double valuePerSquare;
private double squareMeters;
private String typeOfFixed; // einai noiki / katharismos

public Fixed() {}

public Fixed(String code, String descr) {
	super(code,descr);
}

public void setTypeOfFixed(String s) {this.typeOfFixed = s;}
public String getTypeOfFixed() {return typeOfFixed;}

public void setValuePerSquare(double value) {this.valuePerSquare = value;}
public double getValuePerSquare() {return valuePerSquare;}

public void setSquareMeters(double sq) {this.squareMeters = sq;}
public double getSquareMeters() {return squareMeters;}

public void calculateCostPerMonth(){
	System.out.println(valuePerSquare*squareMeters); //kodikas gia miniaio kostos sto pagio
}
}

abstract class FixedPlusUsed extends CostAccount { //klassi pagio kai xrisi
protected double feePerMonth = 6.5; //miniaio pagio logika einai stathera

protected FixedPlusUsed() {}

protected FixedPlusUsed(String code, String descr) {
	super(code,descr);
}
}

class Water extends FixedPlusUsed { //klassi nero
private double cubeMeters;
private double[] valuePerCube = {0.5,0.8}; //timi1 kai timi2

public Water() {}

public Water(String code, String descr) {
	super(code,descr);
}

public void setCubeMeters(double meters) {
	this.cubeMeters = meters;
}

public void calculateCostPerMonth(double cube){ //diaforetiki ylopoihsh sti water
	if (cube < 100) {
		System.out.println(feePerMonth + valuePerCube[0]*cubeMeters);
	} else {
		System.out.println(feePerMonth + valuePerCube[1]*cubeMeters);
	}
}
}

class Telephone extends FixedPlusUsed { //klassi tilefono
private double feeForTelephone = 4.8;
private double pricePerMinuite = 0.2;
private double numOfMin;

public Telephone() {}

public Telephone(String code, String descr) {
	super(code,descr);
}

public void setMinuites(double min) {this.numOfMin = min;}
public double getMinuites() {return numOfMin;}

public void calculateCostPerMonth() {
	System.out.println(feePerMonth + feeForTelephone + pricePerMinuite*numOfMin);
}
}

class Energy extends FixedPlusUsed { //klassi energeia
private double feeForERT = 6.02;
private double pricePerkWh = 0.08;
private double valueOfkWh = 0.009;
private double priceOfZone;
private double squareMeters;

public Energy() {}

public Energy(String code, String descr) {
	super(code,descr);
}

public void setPriceOfZone(double zone) {this.priceOfZone = zone;}
public double getPriceOfZone() {return priceOfZone;}

public void setSquareMeters(double meters) {this.squareMeters = meters;}
public double getSquareMeters() {return squareMeters;}

public void calculateCostPerMonth() {
	System.out.println(feePerMonth + feeForERT + (priceOfZone*squareMeters) + pricePerkWh*valueOfkWh);
}
}

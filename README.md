# PSMod_Root
For plot of the corners 

//   In a ROOT session, you can do:
//      root> .L PSMod.C
//      root> PSMod t
//      root> t.GetEntry(12); // Fill t data members with entry number 12
//      root> t.Show();       // Show values of entry 12
//      root> t.Show(16);     // Read and show values of entry 16
//      root> t.Loop();       // Loop on all entries
//

//     This is the loop skeleton where:
//    jentry is the global entry number in the chain
//    ientry is the entry number in the current Tree
//  Note that the argument to GetEntry must be:
//    jentry for TChain::GetEntry
//    ientry for TTree::GetEntry and TBranch::GetEntry
//
//       To read only selected branches, Insert statements like:
// METHOD1:
//    fChain->SetBranchStatus("*",0);  // disable all branches
//    fChain->SetBranchStatus("branchname",1);  // activate branchname
// METHOD2: replace line
//    fChain->GetEntry(jentry);       //read all branches
//by  b_branchname->GetEntry(ientry); //read only this branch

#define PSMod_cxx
#include "PSMod.h"
#include <TH2.h>
#include <TStyle.h>
#include <TCanvas.h>

void PSMod::Loop(TH2F* Marker1C1,  TH2F* Marker2C1,  TH2F* Marker1C2, TH2F* Marker2C2, TH2F* Marker1C3, TH2F* Marker2C3, TH2F* Marker1C4, TH2F* Marker2C4) 
{

  if (fChain == 0) return;

  Long64_t nentries = fChain->GetEntriesFast();

  Long64_t nbytes = 0, nb = 0;
  for (Long64_t jentry=0; jentry<nentries;jentry++) {
    Long64_t ientry = LoadTree(jentry);
    if (ientry < 0) break;
    nb = fChain->GetEntry(jentry);   nbytes += nb;
    vector<float> myVectorX;
    vector<float> myVectorY;
  
    // if (Cut(ientry) < 0) continue;
    /* 
       Just for remembering
       X1 = MeasurementInfo[0].coordinates; //0
       Y1 = MeasurementInfo[1].coordinates; //0
       X2 = MeasurementInfo[2].coordinates; //-97.751
       Y2 = MeasurementInfo[3].coordinates; //0.777
       X3 = MeasurementInfo[4].coordinates; //-98.12
       Y3 = MeasurementInfo[5].coordinates; //-47.523
       X4 = MeasurementInfo[6].coordinates; //-0.379
       Y4 = MeasurementInfo[7].coordinates; //-48.283
       X5 = MeasurementInfo[8].coordinates; //0
       Y5 = MeasurementInfo[9].coordinates; //0.019
       X6 = MeasurementInfo[10].coordinates; //-1.243
       Y6 = MeasurementInfo[11].coordinates; //-0.008
       X7 = MeasurementInfo[12].coordinates; //-96.494
       Y7 = MeasurementInfo[13].coordinates; //0.81
       X8 = MeasurementInfo[14].coordinates; //-96.889
       Y8 = MeasurementInfo[15].coordinates; //-47.503
       X9 = MeasurementInfo[16].coordinates; //-1.638
       Y9 = MeasurementInfo[17].coordinates; //-48.293
    */
    
    //translating points to absolute coordinates
    //X1, Y1, X2, Y2 stay the same
  
    float X3new;
    X3new = X3 + X2;

    float Y3new;
    Y3new = Y3 + Y2;

    float X4new;
    X4new = X4 + X3 + X2;

    float Y4new;
    Y4new = Y4 + Y3 + Y2;

    float X5new;
    X5new = X5 + X4 + X3 + X2;

    float Y5new;
    Y5new = Y5 + Y4 + Y3 + Y2;

    float X6new;
    X6new = X6 + X5 + X4 + X3 + X2;

    float Y6new;
    Y6new =  Y6 + Y5 + Y4 + Y3 + Y2;

    float X7new;
    X7new = X7 + X6 + X5 + X4 + X3 + X2;

    float Y7new;
    Y7new = Y7 + Y6 + Y5 + Y4 + Y3 + Y2;

    float X8new;
    X8new = X8 + X7 + X6 + X5 + X4 + X3 + X2;

    float Y8new;
    Y8new = Y8 + Y7 + Y6 + Y5 + Y4 + Y3 + Y2;

    float X9new;
    X9new = X9 + X8 + X7 + X6 + X5 + X4 + X3 + X2;

    float Y9new;
    Y9new = Y9 + Y8 + Y7 + Y6 + Y5 + Y4 + Y3 + Y2;
    
    cout << setprecision(12);
    /*
      cout << "X-Coordinate 1: " << X1 << endl; //0
      cout << "Y-Coordinate 1: " << Y1 << endl; //0
      cout << "X-Coordinate 2: " << X2 << endl; //-97.751
      cout << "Y-Coordinate 2: " << Y2 << endl; //0.777
      cout << "X-Coordinate 3: " << X3new << endl; //-98.12
      cout << "Y-Coordinate 3: " << Y3new << endl; //-47.523
      cout << "X-Coordinate 4: " << X4new << endl; //-0.379
      cout << "Y-Coordinate 4: " << Y4new << endl; //-48.283
      cout << "X-Coordinate 5: " << X5new << endl; //0
      cout << "Y-Coordinate 5: " << Y5new << endl; //0.019
      cout << "X-Coordinate 6: " << X6new << endl; //-1.243
      cout << "Y-Coordinate 6: " << Y6new << endl; //-0.008
      cout << "X-Coordinate 7: " << X7new << endl; //-96.494
      cout << "Y-Coordinate 7: " << Y7new << endl; //0.81
      cout << "X-Coordinate 8: " << X8new << endl; //-96.889
      cout << "Y-Coordinate 8: " << Y8new << endl; //-47.503
      cout << "X-Coordinate 9: " << X9new << endl; //-1.638
      cout << "Y-Coordinate 9: " << Y9new << endl; //-48.293
    */

    myVectorX.push_back(X1);
    myVectorY.push_back(Y1);
    myVectorX.push_back(X2);
    myVectorY.push_back(Y2);
    myVectorX.push_back(X3new);
    myVectorY.push_back(Y3new);
    myVectorX.push_back(X4new);
    myVectorY.push_back(Y4new);
    myVectorX.push_back(X5new);
    myVectorY.push_back(Y5new);
    myVectorX.push_back(X6new);
    myVectorY.push_back(Y6new);
    myVectorX.push_back(X7new);
    myVectorY.push_back(Y7new);
    myVectorX.push_back(X8new);
    myVectorY.push_back(Y8new);
    myVectorX.push_back(X9new);
    myVectorY.push_back(Y9new);

    Marker1C1->Fill(myVectorX[0],myVectorY[0]);
    Marker2C1->Fill(myVectorX[5],myVectorY[5]);
    Marker1C2->Fill(myVectorX[6],myVectorY[6]);
    Marker2C2->Fill(myVectorX[1],myVectorY[1]);
    Marker1C3->Fill(myVectorX[2],myVectorY[2]);
    Marker2C3->Fill(myVectorX[7],myVectorY[7]);
    Marker1C4->Fill(myVectorX[3],myVectorY[3]);
    Marker2C4->Fill(myVectorX[8],myVectorY[8]);
    
    cout << ""<<endl;
    /*
      Horizontal Line for the bottom sensor has points (0,0) to (-97.751,0.777) and (-0.38, -48.283) to (-98.12, -47.523) 
      Legends: 
      bottom sensor upper: M1 (slope), Theta1 (angle)
      bottom sensor lower: M2 (slope), Theta2 (angle)
    */
    cout << "Horizontal Lines for the bottom sensor" << endl;
    double m1HU; //slope bottom sensor upper
    m1HU = Y2/X2;
    cout << "M1: "<< m1HU << endl;

    double thetaHUBottom;
    thetaHUBottom = atan(m1HU);
    cout << "Theta1: " <<  thetaHUBottom << endl;

    double m2HL; //bottom sensor lower
    m2HL = (Y3new - Y4new)/(X3new - X4new); //bottom sensor 
    cout << "M2: " << m2HL << endl;

    double thetaHLBottom;
    thetaHLBottom = atan(m2HL);
    cout << "Theta2: " <<  thetaHLBottom << endl;

    //Deltatheta
    double DeltaThetaBottom;
    DeltaThetaBottom = abs(thetaHUBottom - thetaHLBottom);
    cout<<"Delta Theta Bottom Sensor: "<< DeltaThetaBottom<< endl;

    /*
      Horizontal Line for the top sensor has points  (-1.243, 0.008) to (-96.494, 0.81) and (-1.638, -48.293) to (-96.889, -47.503)
      Legends: 
      top sensor upper: M3 (slope), Theta3 (angle)
      top sensor slower: M4 (slope), Theta4 (angle)
    */
    cout <<""<<endl;
    cout << "Horizontal Lines for the top sensor" << endl;

    double m2HU; //top sensor 
    m2HU = (Y7new - Y6new)/(X7new - X6new);
    cout << "M3: " << m2HU << endl;

    double thetaHUTop;
    thetaHUTop = atan(m2HU);
    cout << "Theta3: " <<  thetaHUTop << endl;

    double m1HL;
    m1HL = (Y9new - Y8new)/(X9new - X8new); //top sensor 
    cout << "M4: "<< m1HL << endl;

    double thetaHLTop;
    thetaHLTop = atan(m1HL);
    cout << "Theta4: " <<  thetaHLTop << endl;

    double DeltaThetaTop;
    DeltaThetaTop = abs(thetaHUTop - thetaHLTop);
    cout<<"Delta Theta Top Sensor: "<< DeltaThetaTop<< endl;
  
    cout <<""<<endl;
    cout<<"Some other checks" << endl; //The difference between the outer marker from the inner marker is 1.25mm

    double Corner1;
    Corner1 = abs(X6new - X1);
    cout << "Corner 1: " << Corner1 << endl;

    double Corner2;
    Corner2 = abs(X2 - X7new);
    cout << "Corner 2: " << Corner2 << endl;

    double Corner3;
    Corner3 = abs(X3new - X8new);
    cout << "Corner 3: " << Corner3 << endl;

    double Corner4;
    Corner4 = abs(X9new - X4new);
    cout << "Corner 4: " << Corner4 << endl;  
  }
}
//The overall controlling function
int run(){
  PSMod m;
  //Creating the Histograms
  TH2F* Marker1C1= new TH2F("Marker1C1", "Corner 1", 200, -1.5,0.5, 200, -0.5,0.5);
  TH2F* Marker2C1= new TH2F("Marker2C1", "Corner 1", 200, -2,2, 200, -2,2); //-2,2, 200, -2,2
  TH2F* Marker1C2= new TH2F("Marker1C2", "Corner 2", 200, -98.5,-96, 200, 0,1.6); //2, -96,-98, 2, 0.5,2
  TH2F* Marker2C2= new TH2F("Marker2C2", "Corner 2", 200, -98.5,-96, 200, 0,1.6);
  TH2F* Marker1C3= new TH2F("Marker1C3", "Corner 3", 200, -98.5,-96.5, 200, -54,-40);
  TH2F* Marker2C3= new TH2F("Marker2C3", "Corner 3", 200, -98.5,-96.5, 200, -54,-40);
  TH2F* Marker1C4= new TH2F("Marker1C4", "Corner 4", 200, -2,0, 200, -52,-44);
  TH2F* Marker2C4= new TH2F("Marker2C4", "Corner 4", 200, -2,0, 200, -52,-44);
  
  
  //Run the object's Loop() function
  m.Loop(Marker1C1,  Marker2C1,  Marker1C2,  Marker2C2,  Marker1C3,  Marker2C3,  Marker1C4,  Marker2C4); 
  TCanvas* c1 = new TCanvas("c1", "Module Marker Corners", 800, 600);
  c1->Divide(2,2);
  c1->cd(1);
  Marker1C1->Draw();
  Marker2C1->Draw("SAME");
  c1->cd(2);
  Marker1C2->Draw();
  Marker2C2->Draw("SAME");
  c1->cd(3);
  Marker1C3->Draw();
  Marker2C3->Draw("SAME");
  c1->cd(4);
  Marker1C4->Draw();
  Marker2C4->Draw("SAME");
  c1->Print("ModuleMarkeruno.pdf");
 
  TFile f("ModuleCornersnew.root", "Recreate");
  f.cd();
  gStyle->SetOptStat(111111);
 
  Marker1C1->GetXaxis()->SetTitle("mm");
  Marker1C1->GetYaxis()->SetTitle("mm");
  Marker1C1->Write();

  Marker2C1->GetXaxis()->SetTitle("mm");
  Marker2C1->GetYaxis()->SetTitle("mm");
  Marker2C1->Write();

  Marker1C2->GetXaxis()->SetTitle("mm");
  Marker1C2->GetYaxis()->SetTitle("mm");
  Marker1C2->Write();

  Marker2C2->GetXaxis()->SetTitle("mm");
  Marker2C2->GetYaxis()->SetTitle("mm");
  Marker2C2->Write();

  Marker1C3->GetXaxis()->SetTitle("mm");
  Marker1C3->GetYaxis()->SetTitle("mm");
  Marker1C3->Write();

  Marker2C3->GetXaxis()->SetTitle("mm");
  Marker2C3->GetYaxis()->SetTitle("mm");
  Marker2C3->Write();

  Marker1C4->GetXaxis()->SetTitle("mm");
  Marker1C4->GetYaxis()->SetTitle("mm");
  Marker1C4->Write();

  Marker2C4->GetXaxis()->SetTitle("mm");
  Marker2C4->GetYaxis()->SetTitle("mm");
  Marker2C4->Write();
  
  delete Marker1C1;
  delete Marker2C1;
  delete Marker1C2;
  delete Marker2C2;
  delete Marker1C3;
  delete Marker2C3;
  delete Marker1C4;
  delete Marker2C4;
  
 
  return 0;
}

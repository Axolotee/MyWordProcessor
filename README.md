# MyWordProcessor
package Swing;

import java.awt.*;
import java.awt.event.InputEvent;
import java.awt.event.KeyEvent;
import javax.swing.*;
import javax.swing.text.StyledEditorKit;

public class MyWordProcessor {

	public static void main(String[] args) {

		MarcoPractica mimarco=new MarcoPractica();
		mimarco.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
}

class MarcoPractica extends JFrame{
	
	public MarcoPractica(){
		
		setBounds(600,300,600,350);
		
		setTitle("Practica 1");
		
		laminaPractica milamina=new laminaPractica();
		
		add(milamina);
		
		setVisible(true);
		}
}

class laminaPractica extends JPanel{ 
	
	public laminaPractica (){
		
		setLayout(new BorderLayout());
		
		JPanel laminaMenu = new JPanel();
		
		add(laminaMenu,BorderLayout.NORTH);
		
		JMenuBar barraPrincipal = new JMenuBar();
		
		fuente = new JMenu("Fuente");
		estilo = new JMenu("Estilo");
		tamagno = new JMenu("Tamaño");
		
		barraPrincipal.add(fuente);
	    barraPrincipal.add(estilo);
		barraPrincipal.add(tamagno);
		
		//--------------------------------------------------
		
		configura_menu("fuente","Arial","Arial",9,12,"");
		configura_menu("fuente","Courier","Courier",9,12,"");
		configura_menu("fuente","Verdana","Verdana",9,12,"");
		
		//--------------------------------------------------
		
		JCheckBoxMenuItem negrita= new JCheckBoxMenuItem("Negrita",new ImageIcon("bin/Swing/bold.gif"));
		JCheckBoxMenuItem cursiva= new JCheckBoxMenuItem("Cursiva",new ImageIcon("bin/Swing/italic.gif"));
		
		estilo.add(negrita);
		estilo.add(cursiva);
		
		negrita.addActionListener(new StyledEditorKit.BoldAction());
		cursiva.addActionListener(new StyledEditorKit.ItalicAction());
		
		//--------------------------------------------------
		
		ButtonGroup tamagno_letra=new ButtonGroup();
		
		JRadioButtonMenuItem doce=new JRadioButtonMenuItem("12");
		JRadioButtonMenuItem catorce=new JRadioButtonMenuItem("14");
		JRadioButtonMenuItem dieciseis=new JRadioButtonMenuItem("16");
		JRadioButtonMenuItem veinte=new JRadioButtonMenuItem("20");
		
		tamagno_letra.add(doce);
		tamagno_letra.add(catorce);
		tamagno_letra.add(dieciseis);
		tamagno_letra.add(veinte);
		
		doce.addActionListener(new StyledEditorKit.FontSizeAction("cambio tamaño", 12));
		catorce.addActionListener(new StyledEditorKit.FontSizeAction("cambio tamaño", 14));
		dieciseis.addActionListener(new StyledEditorKit.FontSizeAction("cambio tamaño", 16));
		veinte.addActionListener(new StyledEditorKit.FontSizeAction("cambio tamaño", 20));
		
		doce.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_1,InputEvent.CTRL_DOWN_MASK));
		catorce.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_2,InputEvent.CTRL_DOWN_MASK));
		dieciseis.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_3,InputEvent.CTRL_DOWN_MASK));
		veinte.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_4,InputEvent.CTRL_DOWN_MASK));
		
		tamagno.add(doce);
		tamagno.add(catorce);
		tamagno.add(dieciseis);
		tamagno.add(veinte);
		
		
		//---------------------------------------------------
		
		laminaMenu.add(barraPrincipal);
		
		miTexto = new JTextPane();
		
		add(miTexto,BorderLayout.CENTER);
		
		JPopupMenu emergente=new JPopupMenu();
		
		JMenuItem opcion1 = new JMenuItem ("Bold");
		
		JMenuItem opcion2 = new JMenuItem ("Italic");
		
		opcion1.addActionListener(new StyledEditorKit.BoldAction());
		opcion2.addActionListener(new StyledEditorKit.ItalicAction());
		
		emergente.add(opcion1);
		emergente.add(opcion2);
		
		miTexto.setComponentPopupMenu(emergente);
		
		barra=new JToolBar();
		
		configura_barra("bin/Swing/bold.gif").addActionListener(new StyledEditorKit.BoldAction());
		
		barra.addSeparator();
		
		configura_barra("bin/Swing/verde.gif").addActionListener(new StyledEditorKit.ForegroundAction("ponVerde", Color.GREEN));
		
		barra.addSeparator();
		
		configura_barra("bin/Swing/centro.gif").addActionListener(new StyledEditorKit.AlignmentAction("centrado", 1));
		
		barra.setOrientation(1);
		
		add(barra,BorderLayout.WEST);
		
	}
	
	public JButton configura_barra(String ruta){
		
		JButton boton =new JButton(new ImageIcon(ruta));
		
		barra.add(boton);
		
		return boton;
	}
	
	public void configura_menu(String menu, String rotulo, String letra, int tipo, int tam, String ruta_icono){
		
		JMenuItem elemento = new JMenuItem(rotulo, new ImageIcon(ruta_icono));
		
		if(menu=="fuente"){
			
			fuente.add(elemento);
			
			if(letra=="Arial"){
				
				elemento.addActionListener(new StyledEditorKit.FontFamilyAction("cambiar letra", "Arial"));
				
			}else if(letra=="Verdana"){
				
				elemento.addActionListener(new StyledEditorKit.FontFamilyAction("cambiar letra", "Verdana"));
				
			}else{
				
				elemento.addActionListener(new StyledEditorKit.FontFamilyAction("cambiar letra", "Courier"));
			}
			
		}else if(menu=="tamaño"){
				
			tamagno.add(elemento);
			
			elemento.addActionListener(new StyledEditorKit.FontSizeAction("cambia texto", tam));
		}
	
	}
	

	JMenu fuente, estilo, tamagno;

	JTextPane miTexto;
	
	Font letras;
	
	JButton negritaBarra, cursivaBarra, subBarra, azulBarra, amarilloBarra, verdeBarra, izqbarra, centbarra, dechbarra, justbarra;
	
	JToolBar barra;
	
}

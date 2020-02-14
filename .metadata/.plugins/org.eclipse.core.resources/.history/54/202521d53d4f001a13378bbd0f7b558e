import java.util.HashMap;
import java.util.Map;
import java.util.List;

import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

import org.jbpm.test.JBPMHelper;
import org.kie.api.KieBase;
import org.kie.api.KieServices;
import org.kie.api.runtime.KieContainer;
import org.kie.api.runtime.KieSession;
import org.kie.api.runtime.manager.RuntimeEngine;
import org.kie.api.runtime.manager.RuntimeEnvironmentBuilder;
import org.kie.api.runtime.manager.RuntimeManager;
import org.kie.api.runtime.manager.RuntimeManagerFactory;
import org.kie.api.task.TaskService;
import org.kie.api.task.model.TaskSummary;

public class VendedorMain {
	
	
	public static void main(String args[]) {
		
		 KieServices kieServices = KieServices.Factory.get();
		 KieContainer kContainer = kieServices.getKieClasspathContainer();
		 KieBase kbase = kContainer.getKieBase("myKieBase");
	
		 Map<String, Object> params = new HashMap<String, Object>();
		 
		 params.put("sales", 20000);

	        
		 RuntimeManager manager = createRuntimeManager(kbase);
		 RuntimeEngine engine = manager.getRuntimeEngine(null);
		 KieSession ksession = engine.getKieSession();
		 
			 
		 ksession.startProcess("com.sample2.bpmn",params);
		 ksession.signalEvent("SomeEvent", null);
		 ksession.dispose();
			
	}
	
	
	
	private static RuntimeManager createRuntimeManager(KieBase kbase) {
		JBPMHelper.startH2Server();
		JBPMHelper.setupDataSource();
		EntityManagerFactory emf = Persistence.createEntityManagerFactory("org.jbpm.persistence.jpa");
		RuntimeEnvironmentBuilder builder = RuntimeEnvironmentBuilder.Factory.get()
			.newDefaultBuilder().entityManagerFactory(emf)
			.knowledgeBase(kbase);
		
		System.out.println("adsadsadas");
		return RuntimeManagerFactory.Factory.get()
			.newSingletonRuntimeManager(builder.get(), "vendedor:1.0");
	}
	
	

}
